NCL PGP Lookup: The Ultimate Angle Guide  

**1\. The Standard Search Angle (Keyserver Discovery)**

The most common task is finding a specific key based on an email address or a name.

- **The Trap:** Not all keyservers sync perfectly. If you can't find a key on one, you **must** check others.
- **Key Platforms:**
  - [**Ubuntu Keyserver**](https://keyserver.ubuntu.com/)**:** The "go-to" for most NCL challenges.
  - [**MIT PGP Server**](https://pgp.mit.edu/)**:** One of the oldest; often used for legacy-style challenges.
  - [**OpenPGP.org**](https://keys.openpgp.org/)**:** A cleaner, modern alternative.

**2\. The Identification Angle (Fingerprints & IDs)**

NCL will often give you a "Fingerprint" and ask for the "Key ID," or vice versa.

- **Fingerprint:** A 40-character hex string (e.g., 7A39 A56B 73D1 E097 D574 35CF CDE2 DE1D CB20 77F2).
- **Long Key ID:** The **last 16 characters** of the fingerprint.
- **Short Key ID:** The **last 8 characters** of the fingerprint.
  - _Note:_ Short IDs are considered insecure due to collision attacks, but NCL may still use them for simpler "Easy" tier questions.

**3\. The Metadata Angle (Timelines & Forensics)**

Once you find a key, the challenge might ask for specific data points buried in the record:

- **Creation Date vs. Expiration Date:** Ensure you don't mix up Cr. Time (when it was made) and Key Expir (when it dies).
- **UTC Conversions:** NCL flags are almost always requested in **UTC**. If the keyserver shows a timestamp in a different format, you may need to convert it.
- **Subkeys:** A single PGP "Certificate" can have multiple subkeys (one for signing, one for encryption). NCL might ask for the fingerprint of the _specific_ subkey used for encryption.

**4\. The "Import & Inspect" Angle (CLI Tools)**

In higher-tier challenges, the keyserver might not show all the info in the web UI, or you might be given an .asc file (a "Public Key Block"). You'll need to use the command line:

- **Import the key:** gpg --import keyfile.asc
- **List with fingerprints:** gpg --list-keys --fingerprint
- **Check for signatures:** gpg --list-sigs \[KeyID\]
  - _Angle:_ NCL might ask "Who signed this key?" to test your understanding of the **Web of Trust**. You'd look for other UIDs that have "signed" the target key.

**5\. The Decryption Angle (The "Flag" in the Message)**

Sometimes the PGP lookup is just a prerequisite. You find the Public Key to verify a signature, or you find a **Private Key** (rare, usually hidden in a separate forensics challenge) to decrypt a message containing the flag.

- **Common Scenario:** You find a message that looks like -----BEGIN PGP MESSAGE-----. To read it, you must find the owner's name or email via the Key ID listed in the message header.

**Summary Table: PGP Terms to Know**

| Field | What to look for in the Flag |
| --- | --- |
| **UID** | Usually Name &lt;<email@domain.com>&gt;. |
| **Fingerprint** | 40-character Hex string (no spaces usually). |
| **Algo** | Usually RSA, DSA, or ELG-E. |
| **Key Size** | Common values: 2048, 3072, or 4096. |

**Process**

**1\. Importing the Public Key**

If NCL gives you a .asc or .pub file, or if you copy a block of text starting with -----BEGIN PGP PUBLIC KEY BLOCK-----, save it to a file (e.g., key.asc) and run:

Bash

gpg --import key.asc

**2\. Inspecting the Key Details**

To find the email, fingerprint, and subkeys (the "angles" NCL loves), use the list command with the fingerprint flag:

Bash

gpg --list-keys --fingerprint

**What the output tells you:**

- **pub:** The public key. The number next to it (e.g., 4096R) is the **Key Size** and **Algorithm**.
- **uid:** This is the **User ID**. It contains the name and email address.
- **sub:** These are **Subkeys**. NCL might ask for the specific ID of the encryption subkey.
- **Key Fingerprint:** The long string of hex characters.

**3\. Extracting Hidden Metadata (The "Packets" Angle)**

Sometimes NCL hides information in the packet structure of the key that doesn't show up in a standard list. To see the "raw" guts of a PGP key, use:

Bash

gpg --list-packets key.asc

- **Why this matters:** This can show you the **version** of PGP used, the specific **symmetric algorithms** supported (AES256, etc.), and exact **Unix timestamps** for creation.

**4\. Finding the Key ID from an Encrypted Message**

If you are given an encrypted message (message.asc) and need to know which public key to look up on a keyserver, run:

Bash

gpg --list-only --metadata --decrypt message.asc

- **The Result:** It will tell you something like anonymous recipient; to: ID 0xABC123.... That **ID** is what you plug into the search bar at keyserver.ubuntu.com.

**NCL Command Cheat Sheet**

| Task | Command |
| --- | --- |
| **Search Keyserver** | gpg --keyserver keyserver.ubuntu.com --search-keys <email@domain.com> |
| **Download Key** | gpg --keyserver keyserver.ubuntu.com --recv-keys \[KeyID\] |
| **Export to Text** | gpg --armor --export \[KeyID\] > publickey.asc |
| **Check Signatures** | gpg --list-sigs \[KeyID\] (Shows who "trusts" this user) |
