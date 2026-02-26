# Packet Dissection

## [Cyberchef](https://cyberchef.io/)

Cyberchef is a website where you can encode, decrypt, translate bases, and more. For this challenge, we will be using binary and hex to translate the binary seen in the packet that we are given.

## Challenge

1. **What is the header checksum in hexadecimal representation?**

    For this challenge, we are given 20 boxes of binary in a table. We will need to do the following to figure out what this means in hexadecimal

    * Find the binary that makes the header checksum (in this case, column 3, rows 3 and 4)
    * Go to Cyberchef
    * Copy the binary into the input box
    * Select recipes `From Binary` and `To Hex` **(It must be in that order)**
    * Keep the bytes per line number for `To Hex` at 0 and set the byte length for `From Binary` to 8

2. **What is the TTL of the packet?**

    TTL stands for Time to Live. To find this, we will need to do the following

    * Find the binary that will be in column 3, row 1
    * Paste the binary into the input box in Cyberchef
    * Remove the `To Hex` recipe and replace it with `To Decimal`
    * Keep the byte length at 8

3. **What is the source IP address?**

    Packets reserve source IPs in its 4th column.

    * Paste all rows of binary in column 4 to Cyberchef
    * Apply `From Binary`, `To Hex`, and `Change IP format` in that order
    * Set the byte limit for `From Binary` to 8
    * Set the Input Format to Hex for `Change IP format`

4. **What is the destination IP address?**

    Since packets reserve destination IPs in its 5th column, you will do the same process as question 3, except you will paste all rows of binary in column 5 to Cyberchef.