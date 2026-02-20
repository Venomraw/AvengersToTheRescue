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

If present → the file is actually PNG, not JPEG.

### Fix the header
Open the file in a hex editor and replace the first 12 bytes with:

89 50 4e 47 0d 0a 1a 0a 00 00 00 0d

Another way to do this is to use `xxd flag.jpg > hex.txt`  
then edit the hex.txt with vim and use `xxd -r hex.txt > flag.jpeg`  
-r = revert

Rename the file:

`mv flag.jpeg flag.png`

Open the image:

 `xdg-open flag.png`
