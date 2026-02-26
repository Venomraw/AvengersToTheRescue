# HTTP

## Wireshark

We will be using [Wireshark](https://www.wireshark.org/) for this challenge.

Wireshark is a network protocol analyzer, which we can use to examine the pcap file given in the challenge.

## Challenge

1. **What Linux tool was used to execute a file download?**

    For this question, we need to find what command was used to request a file for download. In the HTTP protocol, the user will send a `GET` packet. In order to find this, we need to do the following in Wireshark.

    * Go to File and open the pcap file
    * Find the packet that uses the HTTP protocol with `GET` in the info tab
    * Once found, click on the Hypertext Transfer Protocol arrow
    * Find the command used to initiate the `GET` request

2. **What is the name of the web server software that handled the request?**

    Now we'll need to find the packet that completed the download.

    * Scroll down to the HTTP packet that contains an `OK` message
    * Click the Hypertext Transfer Protocol arrow
    * Look beneath `HTTP/1.1` for Server to find the answer

3. **What IP address initiated request?**

    In the same packet, look for the IP under the Source tab.

4. **What is the IP address of the server?**

    This works the same way as in number 3, except you look under the Destination tab.

5. **What is the md5sum of the file downloaded?**

    We will need to download the image in order to do an md5sum. To do this, we will do the following

    * Keep the packet from questions 2, 3, and 4 highlighted
    * Click File in the top left
    * Click Export Objects
    * Click HTTP
    * Save the file in a place of your choosing
    * Open a Linux Terminal
    * Type `md5sum (insert file here)`