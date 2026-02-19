# Magic Bytes 

### Goal

Repair a tampered image by fixing the file signature and recover the
flag.

### Tools

-   CyberChef
-   Hex editor (HxD / Bless / GHex)

### Identify the real format

Use CyberChef → **Strings**

Look for PNG markers:

IHDR  
IDAT

If present → the file is actually **PNG**, not JPEG.

### Fix the header

Open the file in a hex editor and replace the first 12 bytes with:

89 50 4E 47 0D 0A 1A 0A 00 00 00 0D

Rename the file:

`mv flag.jpeg flag.png`

Open the image:

 `xdg-open flag.png`
