# Windows and PDF Password Cracking

Notes for using tools to crack passwords for Windows and PDF files.

## Password Cracking Tools

- **John The Ripper**: Free password cracking tool that can quickly extract password from a variety of hash types.

- **Ophcrack**: A password cracker program for Windows that is completely free. Utlizes rainbow tables for cracking passwords. Useful for cracking NT and LM password hashes.

### Where to Install

- For `john`, in linux install using terminal.

    `sudo apt install john`

- For ophcrack you can visit this website to install.

    [Ophcrack Website](https://ophcrack.sourceforge.io/download.php?type=ophcrack)

## PDF Password Cracking with John

### Using PDF2John

- When using `john` for cracking the password of an encrypted PDF file, extracting the password hash come first:

    `pdf2john encrypted.pdf > hash.txt`

- `pdf2john` command is use to extract from a encrypted PDF file, specifically to get the password hashes.

- In some cases especially in WSL, `pdf2john` command may not work even though `john` has already been installed. 
- One solution to this is install the `pdf2john` script in your directory:

    `wget https://raw.githubusercontent.com/openwall/john/bleeding-jumbo/run/pdf2john.py`

- Use python to use `pdf2john`:

    `python3 path/to/file/pdf2john.py encrypted.pdf > hash.txt`

### Using Rockyou Wordlist

- Rockyou wordlist provies a long list of password
- Useful to help crack the password hash from the created hash.txt using `john`:

    `john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`

- Install the rockyou.txt if it doesn't exist in the directory

    `wget https://github.com/mkijowski/passwords/raw/master/dictionaries/rockyou.txt.gz`

### Viewing Crack Password

- Once completed, the cracked password can be fully viewed:

    `john --show hash.txt`

- For this case after cracking the passsword for encrypted.pdf, it should show something like this:

    ```
    john --show hash.txt
    ?:keanureeves2008

    1 password hash cracked, 0 left
    ```
### Gym Challenges for PDF Cracking

1. What is the password used to encrypt the pdf?

    `keanureeves2008`

2. What is the flag in the PDF?

    Picture of sad Keanue Reeves.

## Windows Password Cracking with Ophcrack

### XP Rainbow Tables

- Variety of tables that help with cracking windows passwords
- Recommended to install XP special wordlist for the usage of special characters for password cracking.

### Setting Up ophcrack

- Open ophcrack program
- Click "Tables" and select "XP special"
- Click "install"
- Locate the folder you install the XP special files
- Click ok

## Password Cracking using ophcracck

- Click "Load" on the top left corner.
- For loading only one hash, click "Single Hash" and input the hash.
- If there is a text file that contains a list of hashes select "PWDUMP file" to load them all.
- Click "Crack" on the top middle corner to start cracking the password.
- Once finish, crack password should be shown on the left side
- Recommend to use the NT Pwd column since it contain the complete passsword and used on modern window systems


### Windows Hash Password Locations

- The hash passwords for windows are located at `C:\windows\system32\config\SAM`
- Placed in the the SAM(Security Account Manager) registry hive.

### Gym Challenges For Windows

1. 21259DD63B980471AAD3B435B51404EE:1E43E37B818AB5EDB066EB58CCDC1823

    `^B7e3D;`

2. 11CB3F697332AE4C4A3B108F3FA6CB6D:13B29964CC2480B4EF454C59562E675C

    `yhM^GK7`

3. 65711C079DC4CD3CC2265B23734E0DAC:47F747C5190DC0F0B921AA4A07F06285

    `starf0x`

4. FBBDA33FC12E83FB0C240E84A183686E:DDE9DC6E34E2E6E11EF9E51C6B27ED96

    `P@ssword`

5. 21C4E7C2EFE8E8D1C00B70065ED76AA7:A7A0F9AFD4A78F531A1CF4C42E531BBF

    `footba11`

6. E85B4B634711A266AAD3B435B51404EE:FD134459FE4D3A6DB4034C4E52403F16

    `ectoplasm32`

7. BA756FB317B622DBAAD3B435B51404EE:C8405270B10B13AE8A24612BB853567A

    `58?-<C6`

8. 199C926FA387EAB7AAD3B435B51404EE:F196F77BF8BB15781BA8364C649C5FD4

    `1trustno1`

9. FE4AACAAAD7D986AAAD3B435B51404EE:3928E16F614E2316CA51C336FA5B3011

    `$xEn@=y`

10. 3613F7EC15407F56AAD3B435B51404EE:C82E164316183AA3AF3EA6BAA642A237

    `"=Cxu&L`


