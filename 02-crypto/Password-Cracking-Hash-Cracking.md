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

## 500 Passwords List

### What is it?

The 500 passwords as the name says, contains the 500 most common passwords in one file.

### What is in the list?

The list contains weak passwords. Most of the passwords contained are locations, names, things, numbers, and simple words.

- A few passwords in the list include the following
    
    * `football`
    * `dragon`
    * `1234567`
    * `qwerty`
    * `password`

### Why have the list?

The list can be used to do quick hash cracking and can also be used as what your password shouldn't be. You can find the list [here](https://www.scribd.com/document/723645137/500-most-commonly-used-password)

---

## rockyou.txt

### What is rockyou.txt?

rockyou.txt is the most common word list used to crack passwords/hashes, with the list containing over 14 million passwords, most of which are weak passwords.

### Why does this list exist?

Rockyou is a company that was desolved in 2019 that created widgets for MySpace and Facebook founded in 2005. In 2009, Rockyou had a data breach where over 32 million accounts got compromised and over 14 million passwords were leaked. The reason the breach caused that many passwords to be exposed was because Rockyou stored their users passwords in a SQL database without encrypting them. The person(s) responsable for the breach used an old SQL vulnerability that Rockyou did not update to patch, which resulted in rockyou.txt to be formed

### Where to Find rockyou.txt?

Because rockyou.txt is ~133MB in size, I will not include it in the repository. You can find the rockyou.txt [here](https://www.kaggle.com/datasets/wjburns/common-password-list-rockyoutxt)

---

## Pokemon Gym Challenge

In the challenge, it tells me to use hashcat, but I will only use John The Ripper since that is what Matt wants.

### Question

#### Solve the following hashes

```
1. a532443f3e04a9e00295a8cd2a75e080
2. 54c10b9736b70e75c6e505f340b6e2f1
3. b8a24794813a47521b4be55747e0665a
4. 83b020b0a7b3c353e1c11b1647b53cda
5. 999cae1e22fe69d89d6f56e3050f18cb
```

### Creating the Hash List

To create the hash list, I will be putting the hashes above into a `.txt` file named `hashes.txt`. I will be using Linux to do this challenge, so I will type `vim hashes.txt` to create the file and paste the hashes into the file.

### Creating the Word List

There are already instructions in the challenge for this step, so I will simpily run the command below to have `pokemon.txt` as a word list.

```
curl -s -A "Mozilla/5.0" \
  https://bulbapedia.bulbagarden.net/wiki/List_of_Pokémon_by_National_Pokédex_number \
  | grep 'href="/wiki/.*(Pok' \
  | sed 's/.*">//; s/<\/a.*//;' \
  | sort -u \
  > pokemon.txt
```

This command will create the list of pokemon, but it will only download with the pokemon names being upper case. Since MD5 (The type of hash being used for the hashes) is case sensitive, we need to run `tr 'A-Z' 'a-z' < pokemon.txt > pokemon-lower.txt`. `pokemon-lower.txt` is named for the user to know it contains lower case characters.

### Using John The Ripper to Crack the Hashes

Using the same command in the how to use section of John The Ripper earlier, I will be able to crack the hashes. The command used will be `john --wordlist=pokemon-lower.txt hashes.txt`. **See Note Section If This Does Not Work**

### Answers

Here is the list of what each hash results in

    1. basculin
    2. rotom
    3. celebi
    4. goldeen
    5. golduck

### Note

I couldn't get the command to work using WSL Ubuntu Linux since the version of John The Ripper I used was a core version of the program. So I launched my personal Kali Linux instance where Jumbo John The Ripper comes packaged with and by using the command `john --format=Raw-MD5 --wordlist=pokemon-lower.txt hashes.txt`, I managed to crack the hashes. John by default uses the LM format so if you need to use a different format to crack hashes, use `--format=<Select Format Here>`.

---