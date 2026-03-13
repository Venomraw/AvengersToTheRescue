FTP Notes 
FTP is an old file-transfer protocol to move files that employs two distinct connections: one for control and one for data. The control channel carries commands like USER, PASS, LIST, STOR, RETR, and DELE. The data channel carries file contents and directory-listing data. RFC 959 explains these commands and how FTP works in general.
FTP is considered insecure because credentials and commands are normally sent in plaintext, which means usernames, passwords, filenames, and many actions are often readable directly in a packet capture. Wireshark’s FTP page and incident-response references both describe FTP traffic as visible and easy to inspect in captures. 
Important FTP Commands for cyber skyline 
1.	USER = username supplied to server
2.	PASS = password supplied to server
3.	LIST = request a directory listing
4.	STOR = upload a file to the server
5.	RETR = download a file from the server
6.	DELE = delete a file from the server
7.	CWD = change working directory
8.	PWD = print working directory
Important FTP response codes 
1.	220 = server banner / service ready
2.	331 = username accepted, need password
3.	230 = user logged in successfully
4.	226 = closing data connection / transfer completed
5.	550 = requested action not taken, often file not found or access denied
Possible Tools to Use:
1)	Wireshsark 
2)	Tshark
3)	Cloudshark

Used: Wireshark 
In Wireshark, Follow TCP Stream puts the discussion back together for one TCP session in the right order. Wireshark uses a display filter for that stream and shows the data in order. This is exactly why it is great for FTP usernames, passwords, commands, and server banners.
First things to look into the packets are : 
•  the server banner
•  login attempts
•  successful authentication
•  post-login commands
•  filenames involved in upload/download/delete actions
Some of the display filters to use are: 
o	ftp → control-channel FTP packets
o	ftp-data → FTP data-channel packets
o	ftp || ftp-data → both control and data traffic
o	ftp.response.code == 230 → successful logins
o	tcp.stream eq X → isolate one TCP stream once you know its stream number


GYM CHALLENGES: 
1.	What was the first username:password combination attempt made to log in to the server? ex. 'user:password'? 
ANS: Right-click the first packet and choose
Follow then TCP Stream.
In that stream:
The first line usually shows the FTP server banner and software/version 
user1:cyberskyline
2.	What software is the FTP server running? (Name and version) 
ANS: USER and PASS lines show the first username:password attempt 
        FileZilla Server 0.9.53 beta
3.	What is the first username:password combination that allows for successful authentication? 
ANS: Find the first time you see a successful code, then record that USER/PASS pair.
user1:metropolis
4.	What is the first command the user executes on the ftp server?
ANS: Find the first FTP command sent by client after the first successful 230 response.
PORT
5.	What file is deleted from the ftp server?
ANS: Look for FTP command:
DELE <filename>
bank.cap
6.	What file is uploaded to the ftp server? 
ANS: Look for command: STOR <filename>
compcodes.zip
7.	What is the filesize (in bytes) of the uploaded file? 
ANS: Follow → TCP Stream
    At the bottom Wireshark shows stream bytes, or you can export and check length.
28183 bytes
8.	What file does the anonymous user download?
ANS: Find where user logs in as anonymous:
USER anonymous
Then find download command:
RETR <filename>
compcodes.zip
