# The Book 

Analyze a memory dump to recover any valuable information

### Tools

    xz -d memdump.mem.xz
    volatility2.silf
    `vol2` as an alais 

### Identify the OS

    file memdump.mem
    vol2 -f ./memdump.mem windows.info.Info

### Find computer name and username

`vol2 -f ./memdump.mem windows.envars.Envars`

Look for:

COMPUTERNAME=  
USERNAME=

or try  
`strings memdump.mem | grep -i "USERNAME"` and `strings memdump.mem | grep -i "COMPUTERNAME"`

### Locate user files

`vol2 -f ./memdump.mem windows.filescan FileScan | grep "<username>"`

### Dump the file

mkdir output  
`vol2 -f ./memdump.mem -o ./output windows.dumpfiles.DumpFiles --virtaddr <file_address>`

### Inspect the database

The extracted file will be a SQLite database

sqlite3 output/<database_file>  
.tables  
SELECT * FROM <table_name>;  

Find the real name of the user cloud

### Recover password hash

`vol2 -f ./memdump.mem windows.registry.hashdump.Hashdump`

Copy the NTLM hash

### Crack the password

Use an online NTLM cracker: https://crackstation.net

------------------------------------------------------------------------

Answers
```
1. Windows 10
2. DESKTOP-OT97GG3
3. liber8hacker
4. C:\Users\liber8hacker\Desktop\black_book.db
5. Gloria Hampton
6. avatar2
```
