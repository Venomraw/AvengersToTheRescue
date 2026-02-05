# Password Cracking / Hash Cracking
#### By Colin Brunson

## John The Ripper

**The Following Will Be On The Linux Terminal Version Of John The Ripper**

John The Ripper is a tool used for password and hash cracking. It usually uses word lists to crack passwords/hashes.

### How to Install

Using a Linux system, go to the terminal, type `sudo apt install john`, and it will install.

### How to Use

Before you run commands to use John, you need to have a `.txt` file of a word list and another `.txt` file of hashes. In this case, I will be using `500_passwords.txt` for the word list and `sha512.hashes` for the hash list. To crack the hashes using a basic attack, type in `john --wordlist=500_passwords.txt sha512.hashes` (If the file(s) are outside of the directory you are in, you need to type in the path to the files). After you type the command into the terminal, you will have to wait until the command is finished running.

---

## rockyou.txt

### What is rockyou.txt?

rockyou.txt is the most common word list used to crack passwords containing over 14 million passwords, most of which are weak passwords.

### Why?

Rockyou is a company that was desolved in 2019 that created widgets for MySpace and Facebook founded in 2005. In 2009, Rockyou had a data breach where over 32 million accounts got compromised and over 14 million passwords were leaked. The reason the breach caused that many passwords to be exposed was because Rockyou stored their users passwords in a SQL database without encrypting them. The person(s) responsable for the breach used an old SQL vulnerability that Rockyou did not update to patch, which resulted in rockyou.txt to be formed

### Where to Find rockyou.txt?

Because rockyou.txt is ~133MB in size, I will not include it in the repository. The file is easy to find using a google search.

---

