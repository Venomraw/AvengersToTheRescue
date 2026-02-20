# Magic Bytes 

Repair a tampered image by fixing the file signature and recover the
flag 
Files use magic bytes at the beginning of the file
to identify their format
If these bytes are modified, the operating system may misidentify the
file type or refuse to open it  

### Tools

-   CyberChef
-   Hex editor (HxD / Bless / GHex)
-   Linux Terminal

### Identify the real format

Use CyberChef → Strings
Look for PNG markers:

IHDR  
IDAT

If present → the file is actually PNG, not JPEG

### Fix the header
Open the file in a hex editor and replace the first 12 bytes with:

8950 4e47 0d0a 1a0a 0000 000d

Another way to do this is to use `xxd flag.jpg > hex.txt`  
then edit the hex.txt with vim and use `xxd -r hex.txt > flag.jpeg`  
-r = revert

Rename the file:

`mv flag.jpeg flag.png`

Open the image:

 `xdg-open flag.png`

 ------------------------------------------------------------------------

## Docter

Extract hidden data from a Microsoft Word document container
A `.docx` file is actually a ZIP archive

### Tools

-   xdg-open
-   unzip
-   Linux Terminal

### Verify the file type

`file SuperAwesomeDoc.docx`

Expected:

Zip archive data

### Extract the container

unzip SuperAwesomeDoc.docx -d docx_extracted

-d = the subdirectory that the unziped files will go to 
the defalt is the current directory 

XML = eXtensible Markup Language
XML is a text based format ismilar to HDML it focuses on meaning and organization

There is a media folder that contains all the images for the .docx 

You should see more images than appear in the document The extra image
contains the flag

Open it:

`xdg-open <image>.png`
