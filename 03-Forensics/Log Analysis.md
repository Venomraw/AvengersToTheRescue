**Log Analysis Notes**

Log analysis is the process of gathering, looking at, and making sense of log files made by systems, applications, or devices to figure out what happened inside them. Log analysis shows user, account, IP address, or device did something (for example, the username that signed in, the client IP that hit a website, the device ID, or the session ID).It provides the information regarding the exact date and time of events and the order in which they happened (timestamps helps make a chronology of what happened first, next, and last). It is mostly used to read log files and filter and summarize them to detect patterns:
1.Finding out why things went wrong, problems, and outages
2. Security (find attacks, failed logins, and other strange behavior)
3.Auditing (show what happened and who did it)
4. Usage/performance (traffic spikes, most popular pages, sluggish queries)

Goals : The log files can also provide informations of:

1. Who did something? (user / IP / session)
2. What happened? (success/fail, request type, action)
3. When did it happen? (timestamp, order of events)
4. Where did it come from? (source IP, user agent, URL)
5. How often did it happen? (counts, top values, patterns)

The list of some of the most common commands to be used while solving this

**Viewing logs**

* cat file → print entire file
* less file → best viewer (use /pattern to search)
* head -n 20 file / tail -n 50 file
* tail -f file → follow live logs

**Grep (filter/search)**

* grep "text" file
* grep -i "text" file (ignore case)
* grep -n "text" file (show line numbers)
* grep -v "text" file (exclude matches)
* grep -E "a|b|c" file (extended regex OR)
* grep -R "text" folder/ (recursive)

**Useful patterns**

* IP: grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' file
* “failed” / “invalid” / “error” keywords are common starting points

**Cut (extract columns)**

* cut -d' ' -f1,2,3 file (space-delimited)
* cut -d':' -f1 file (colon-delimited)
* For logs with messy spacing, you often use **awk** instead.

**Awk (best for logs)**

* awk '{print $1,$4,$7}' file
* Filter: awk '$9==404 {print $1,$7}' access.log
* Pattern: awk '/Failed password/ {print $1,$2,$3,$11}' auth.log

**Sort / Uniq (counts)**

* sort file
* sort -nr (numeric reverse)
* uniq (removes duplicates only if sorted first!)
* uniq -c (count occurrences)

# SSH

The SSH log file indicates evidence of a brute-force attack, which is when a lot of failed login attempts are made against a single user account in a short amount of time. The fact that "Failed password" messages keep coming from different IP addresses shows that someone is trying to guess the user's password automatically. This behavior strongly shows that someone is trying to hack the server because real users don't usually try to log in from many IPs in a matter of seconds.

We need to look for a log entry that says "Accepted password" to find out if the attacker was able to get in. The notification  , like   "Accepted Passwords" indicates that the authentication worked and gives the specific IP address that was able to get into the system. Finding this IP is very important since it shows where the breach came from and lets security teams take action, such banning the IP, resetting passwords, and looking into other system activities.

GYM CHALLENGES

To complete this challenge, looking into the content of the given logs is very important.

1. What is the hostname of the SSH server that was compromised?

ANS: Find the hostname, which is listed directly after the timestamp for each entry in the log. (myraptor)

2. What was the first IP address to attack the server?

ANS: Look into the logs for the IP address of the attacker in the first “Failed password” entries. (169.139.243.218) 3.

3. What was the second IP address to attack the server?

ANS: This can be solved in the same way as the previous question by looking at the subsequent “Failed password” entries. (56.13.188.38)

4. What was the third IP address to attack the server?

ANS: This can be solved in the same way as the previous question by looking at the subsequent “Failed password” entries. (30.167.206.91)

5. Which user was targeted in the attack?

ANS: This can be solved by identifying the name of the account that had failed password attempts. Search for “Failed password” and then look for the account name. (Harvey)

6. From which IP address was the attacker able to successfully log in?

ANS: This can be solved by searching for the entry that has “Accepted password”. (30.167.206.91)

# Login

This task is about looking at a log file named login.log that has columns separated by tabs, which makes it easy to use the **cut** command to get certain fields. First, use **ls** to make sure the file is in the right folder. You can use **cat** to see the whole file, but since log files might be extensive, it's easier to use **head** or **tail** to show either the first or last 10 lines (by default). These commands let us rapidly look at the log without having to scroll through the whole file. This can be helpful for log files that have column headers - using **head** instead of **cat** will display the column names and the first few lines of data.

Cyber Skyline Notes

* Piping the **wc** command (short for word count), along with the **-l** flag (lower case L for “lines”) will count the lines in the output:
* To display only the usernames, use the **cut** command with the **-f** flag to extract field 3 (the username column). The default delimiter for **cut** is a tab space.
* The usernames can be sorted alphabetically by piping the output through the command **sort**:
* To list only the unique entries, use the **uniq** command.
* The **-c** flag will show the number of times an entry occurs in the output
* The output can be piped throughcut **-f 1,3** to display the first column (Date and Time) and the third column (usernames).
* To display only the date (without the timestamp), use **cut -d " " -f 1.** This tells **cut** to split the line by spaces (instead of the default tab) and extract the first field.

Gym Challenges:

We need to run the following attached codes in the root directory in the Gym, and can solve the given Gym Challenges

**1. How many total login attempts were made in this log?** cat login.log | wc -l

**2. How many unique usernames appear in this log?**

cat login.log | cut -f 3 | sort | uniq | wc -l

**3. What is the username with the most login attempts?** cat login.log | cut -f 3 | sort | uniq -c |sort -n

**4. How many attempts were made for the username with the most login attempts?** cat login.log | cut -f 3 | sort | uniq -c |sort -n

**5. What is the date with the most login attempts?** cat login.log | cut -f 1 | cut -d " " -f 1 | sort | uniq -c | sort -n

**6. What is the username that had logins from the most unique IP addresses?** cat login.log | cut -f 2,3 | sort | uniq | cut -f 2 | sort | uniq -c | sort -n

# VSFTPD

This challenge is about utilizing basic Linux tools like grep, awk, sort, uniq, head, and tail to look at a VSFTPD (Very Secure FTP Daemon) log file. Most of the time, VSFTPD logs provide timestamps, process IDs (PID), usernames, IP addresses, file paths, and event kinds like login, upload, download, or directory creation. You may use grep to look for activity by a certain user (like ftpuser) and then narrow the results even more by looking for specific actions like "OK UPLOAD" or "mkdir." The head and tail commands let you see the first or last entries without having to scroll through the whole file.

You can use grep and awk together with custom delimiters like commas (,) and periods (.) to look at uploads and find the most prevalent file types. To begin, use awk -F ',' to separate the file path column. Then, use awk -F '.' to get the file extension. Using sort | uniq -c to sort and count displays which types of files show up the most. Using awk, you can also get usernames from a certain column (such the 8th column), and sort | uniq can help you find unique people.

Awk can also do more in-depth analysis by adding up things like the total number of bytes a user has submitted. You can get a running total by taking the file size field and using awk '{s+=$1} END {print s}'. To find suspicious behavior, separate successful login records with a custom delimiter (like double quotes) and get the IP addresses. Then, use sort | uniq -c to find login sources that are strange or happen more than once. These methods help find attackers, strange behavior, and general usage trends in the logs of the FTP server.

**GYM Challenges**

We need to run the following attached codes in the root directory in the Gym, and can solve the given Gym Challenges

1. **What IP address did "ftpuser" first log in from?**

cat vsftpd.log | grep ftpuser

2. **What is the first directory that ftpuser created?**

cat vsftpd.log | grep ftpuser | grep -i mkdir | head -n 1

3. **What is the last directory that ftpuser created?**

cat vsftpd.log | grep ftpuser | grep -i mkdir | tail -n 1

4. **What file extension was the most used by ftpuser?**

cat vsftpd.log | grep ftpuser | grep 'OK UPLOAD' | awk -F ',' '{print $2 }' | awk -F "." '{print $2}' | sort | uniq -c | sort

5. **What is the username of the other user in this log?**

cat vsftpd.log | awk '{print $8}' | sort | uniq

6. **What IP address did this other user log in from?**

cat vsftpd.log | grep jimmy

7. **How many total bytes did this other user upload?**

cat vsftpd.log | grep jimmy | grep 'OK UPLOAD' | awk -F ',' '{print $3 }' | awk '{s+=$1} END {print s}'

8. **How many total bytes did ftpuser upload?**

cat vsftpd.log | grep ftpuser | grep 'OK UPLOAD' | awk -F ',' '{print $3 }' | awk '{s+=$1} END {print s}'

9. **How many total bytes did ftpuser download?**

cat vsftpd.log | grep ftpuser | grep 'OK DOWNLOAD' | awk -F ',' '{print $3 }' | awk '{s+=$1} END {print s}'

10. **Identify the IP address of the suspicious login (the login with no subsequent activity)**

cat vsftpd.log | grep 'OK LOGIN' | awk -F '"' '{print $2 }' | sort | uniq

# Nginx

This challenge is about utilizing fundamental Linux commands like cut, sort, uniq, wc, grep, and awk to look at a nginx access log. The IP address is usually the first entry in nginx logs. You may use cut to get it, then sort and count it with sort | uniq | wc -l to find out how many different people visited the server. At the end of each line, there are HTTP status codes (such 200, 404, and 500). You may use cut with a double quotation (") as a delimiter to get them, since the request portion is in quotes. After being separated, the codes can be counted and sorted to find the most common responses. 
 We can use either cut or awk to extract the request field and inspect HTTP methods like GET and POST. To use cut, first separate the quoted request, and then get the first word (the procedure). The HTTP method is usually the sixth field when using awk, which uses whitespace as the default separator. Sort and use uniq -c to find out how often each method is used, and sort -rn to list them from most to least common. Grep is also good for finding patterns, and the -o option only prints the part of a line that matches.
The backslash (\) is an escape character in the Linux shell, therefore you have to be very careful when looking for raw byte sequences like \x04 or \41. You need to escape it with another backslash (for example, grep '\\41' access.log) so that the shell doesn't change it to ASCII. This makes sure that the log is searched for the exact byte sequence. In general, these commands let you easily retrieve organized data, identify problems, and analyze traffic patterns from nginx logs.

**GYM Challenges**

**1. How many different IP addresses reached the server?**

cat access.log | cut -d " " -f 1 | sort | uniq | wc -l

**2. How many requests yielded a 200 code?**

cat access.log | cut -d '"' -f 3 | cut -d ' ' -f 2 | sort | uniq -c | sort -rn

**3. How many requests yielded a 400 code?**

cat access.log | cut -d '"' -f 3 | cut -d ' ' -f 2 | sort | uniq -c | sort -rn

**4. What IP address rang at the doorbell?**

cat access.log | grep "bell"

**5. What version of the Googlebot visited the website?**

cat access.log | grep "Googlebot"

**6. Which IP address attempted to exploit the Shellshock vulnerability?**

cat access.log | grep '() { :; };'

**7. What was the most popular version of Firefox used for browsing the website?**

cat access.log | egrep -o "Firefox/.\*" | sort | uniq -c

**8. What is the most common HTTP method used?**

cat access.log | awk -F " " '{print $6}' | sort | uniq -c | sort -rn

**9. What is the second most common HTTP method used?**

cat access.log | awk -F " " '{print $6}' | sort | uniq -c | sort -rn

**10. How many requests were for \x04\x01\x00P\xC6\xCE\x0Eu0\x00?**

cat access.log | grep '\\x04\\x01\\x00P\\xC6\\xCE\\x0Eu0\\x00' | wc -l

# History

This challenge is about looking at a SQLite database file (browser.sqlite) to find out what users are doing. sqlite3 browser.sqlite will open the file in the terminal and launch the SQLite application. All the tables in the database by using the .tables command can also be seen. We can also see the data in a specific table by using SELECT \* FROM table\_name; If preferred visual interface, we could also utilize a SQLite viewer with a GUI.

The moz\_places table is very significant since it keeps track of the websites that the user has been to. You can use PRAGMA table\_info(moz\_places); to inspect the structure of the table, which includes column names like "url" and "title." Use SELECT url FROM moz\_places; to see the websites you have visited. We could use filters like WHERE title LIKE '%gmail%' or WHERE title LIKE '%$%' to identify Gmail logins or pages that show Bitcoin pricing.

Things like surfing history, the login pages you visited, and even things like transaction IDs could be found by looking at the URLs and page titles recorded in the database. By pulling cached browser history data directly from the SQLite database, this strategy lets investigators learn more about how users act.

GYM CHALLENGES

1. What did the user search for on craigslist? **bitcoin**

2. What was the current price (USD) of bitcoin when the user was browsing? **$239.5**

3. What Bitcoin exchange did the user log in to? **Coinbase**

4. What is the email that was used to log into the exchange? **b1gbird@gmail.com**

5. What was the ID of the Bitcoin transaction that the user looked at? **5274cfba585a4b5681527a37f95c76340428916bb7480cef6c545f0a28dcd2d7**

6. What was the total BTC value of all the inputs of the Bitcoin transaction? **0.22616302**

7. Which Bitcoin address received the majority of the Bitcoin in the transaction? **18z6bTFjxkXCmhfp8YBetR2wgmoVjXGJZz**

# Squid

**Helpful Tools**

* [Epoch Converter](https://www.epochconverter.com/)
* [Understanding how to use awk to print specific columns](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)
* [How squid logs are formatted](https://www.squid-cache.org/Doc/config/logformat/)

To figure out what people are doing on the web, it's necessary to look at a Squid proxy log. We can use head to look at the first few lines of the log file. The first column shows the epoch time, which is the amount of seconds that have passed since January 1, 1970. We can also use internet tools or the Linux date command to change this timestamp into a date that is able to read. Knowing how the log file is set up makes it easier to figure out what each column means.

To extract specific information, use the awk command can be used and awk '{print $2}' to get the second field, which shows how long the proxy took to execute a request (in milliseconds), and then sort it numerically with sort -n. The third field has the IP addresses of the clients. We could also use awk '{print $3}' | sort | uniq | wc -l to find out how many different IPs used the proxy.

The sixth field has HTTP request methods like GET and POST. We can count them with awk '{print $6}' | sort | uniq -c and use grep to filter all entries that are related to an activity from a specified IP address, such 192.168.0.224.  These basic Linux commands also help  to look at how users are using a Squid proxy log, how requests are being made, and how traffic is moving.

GYM Challenges

1. In what year was this log saved**? (2010)**

2. How many milliseconds did the fastest request take? (**5)**

cat squid\_access.log | awk '{print $2}' | sort -n

3. How many milliseconds did the longest request take? **( 41762)**

cat squid\_access.log | awk '{print $2}' | sort -n

4. How many different IP addresses did the proxy service in this log? **(4)**

cat squid\_access.log | awk '{print $3}' | sort | uniq | wc -l

5. How many GET requests were made? **(35)**

cat squid\_access.log | awk '{print $6}' | sort | uniq –c

6. How many POST requests were made? **(78)**

cat squid\_access.log | awk '{print $6}' | sort | uniq –c

7. What company created the antivirus used on the host at 192.168.0.224? (liveupdate.symantecliveupdate.com)

cat squid\_access.log | grep "192.168.0.224"

8. What URL is used to download an antivirus update? ([http://liveupdate.symantecliveupdate.com/streaming/norton$202009$20streaming$20virus$20definitions\_1.0\_symalllanguages\_livetri.zip](http://liveupdate.symantecliveupdate.com/streaming/norton%24202009%2420streaming%2420virus%2420definitions_1.0_symalllanguages_livetri.zip))

Payments

This challenge involves analyzing a SOAP web server log that contains payment data in XML format. To extract this XML data, we could Use the following commands to save the requests and responses into separate files:

sed -nr 's/PPAPIService: Request: (.\*)/\1/p' payments.log > requests.xml

sed -nr 's/PPAPIService: Response: <\?.\*\?>(.\*)/\1/p' payments.log > responses.xml

After extracting the XML, manually add <xml> at the beginning and </xml> at the end of the file so it can be properly recognized by conversion tools. Once formatted correctly, the XML file can be converted into CSV or Excel format using an online tool like convertcsv. This makes it easier to view, filter, and analyze the payment data using a spreadsheet program.

* The tool to use : [convertcsv.com](https://www.convertcsv.com/xml-to-csv.htm)

GYM Challenges

1. How many transactions are contained in the log?

Count the number of lines that start with PPAPIService: Request: (192)

2. What is the transaction ID of the largest purchase made in the log?

Sort the requests by the order total column to find the largest purchase, then get the transaction ID from the corresponding response (998.6)

3. Which state made the greatest number of purchases?

Get a count of the unique values for the state of the ship-to address (Massachusetts)

# Custom File Format

The SKY log file format was made to capture network traffic data in an effective way. It uses raw binary data to reduce space compared to regular text files. This document uses Big-Endian notation for all of its fields.

Terms

* A int is 32 bits, or 4 bytes
* A long is 64 bits, or 8 bytes
* A timestamp is a 32-bit [Unix Timestamp](https://en.wikipedia.org/wiki/Unix_time), or 4 bytes

Explaination about the terms specification:

Header

The SKY header begins at offset 0 and is comprised of the following fields in order with no padding.

1. Magic Bytes
2. Version Number
3. Creation Timestamp
4. Hostname length
5. Hostname
6. Flag length
7. Flag
8. Number of entries

Tools like CyberChef can be used to open the file, extract the Body section, and format it into readable hex output (for example, splitting it into 16-byte lines and 4-byte columns), which can then be saved as hex.log.

Once the log file is in a text format, it becomes easier to convert the data one column at a time and then rejoin the columns into a completed, human-readable log.

Extraction of the columns

**Column 1:** cat hex.log | cut -d " " -f 1 (then copy it to CyberChef to convert the hex to ipv4) then save the output. It’ll represent the source ip.

**Column 2**: cat hex.log | cut -d " " -f 2 (then copy it to CyberChef to convert the hex to ipv4) then save the output It’ll represent the destination ip.

**Column 3**: cat hex.log | cut -d " " -f 3 (then copy it to CyberChef to convert the hex to date and time ) then save the output. It represents the event time for each entry.

**Column 4:** cat hex.log | cut -d " " -f 4 (then copy it to Cyberchef to convert hex to integer) then, save the output, it represents the event code, port, status, bytes.

paste col1.log col2.log col3.log col4.log > merged.log

**Important Details to remember**

1. Endianness is essential because timestamps and integers may be little-endian. If the values don't appear right, the sequence of the bytes needs to be changed during conversion.
2. While breaking the entry into 16 bytes, which is 4 columns times 4 bytes. It means that every log entry is 16 bytes.
3. Validation check for the number of entries field should match the number of lines obtained when splitting the Body into 16-byte pieces.

Gym Challenges

1. What is the hostname of the server? (**sky-server-711)**
2. What is the plaintext flag in the log file? (**SKY-PARS-7325**)
3. On what date was the file created (in UTC)? **( 2018-03-03)**
4. How many entries are in the log file? **(162)**
5. How many total transferred bytes were recorded in the log? (**811167)**
6. How many unique IP addresses (both senders and receivers) are recorded?**(13)**
7. Which IP address sent the most amount of data**? (229.212.21.212)**  awk '{sums[$1]+=$4} END {for (ip in sums) print sums[ip], ip}' merged.log | sort -n
8. How many total bytes were sent by the above IP address that sent the most amount of data? **(145048 )** awk '{sums[$1]+=$4} END {for (ip in sums) print sums[ip], ip}' merged.log | sort -n
9. What was the busiest day (day with the most bytes transferred)? **(2018-03-23)** awk '{sums[$3]+=$4} END {for (date in sums) print sums[date], date}' merged.log | sort -n
