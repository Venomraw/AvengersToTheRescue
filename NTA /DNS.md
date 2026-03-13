Network Traffic Analysis
DNS Notes
DNS is what enables us to access much of the internet without remembering IP addresses. We can analyze the network packet capture to understand more about DNS. DNS is important in cybersecurity because it can reveal which host a user or malware is trying to access. DNS records can show infrastructure, subdomains, and destination IPs. DNS recording is also vital for keeping an eye on security and protecting against attacks. Cloudflare says the main goal of DNS security is to keep the DNS infrastructure safe and ensure it can withstand attacks.
 To complete this challenge 
Tools to use :
Wireshark 
It is a network protocol analyzer. It enables us to see and record network traffic coming in and out of a device, packet by packet. People use it to figure out what's wrong with their network, look at protocols like DNS, HTTP, TCP, and FTP, see which devices are talking to each other, and learn how networks function. Look into traffic that seems strange. 

Open the pcap in Wireshark or CloudShark and look for the packet with the Info column that says "Standard query." That packet tells us what kind of query it is and what domain it is for. Next, we look for the Standard query answer packet that matches and further open up the answers section to see how many answer records there are, read the TTL, and discover the record for the welcome subdomain.


Gym Challenges: 

1.	What is the type of the DNS query requested? 
ANS: Look in the Question part of the DNS query packet. The type could be A, AAAA, CNAME, MX, or something else. An A record connects a name to an IPv4 address, whereas a AAAA record connects to an IPv6 address. AXFR 

2.	What domain was requested?
ANS: Look for the DNS Name field under the Question section. That is the exact hostname being resolved. The DNS query identifies the domain name the client wants translated into an IP address. Etas.com
3.	How many items were in the response?
ANS: Go to the response packet and expand answers. Count how many answer records are listed there. 4
4.	What is the TTL for all of the DNS records?
ANS: TTL means Time To Live. In DNS, TTL is the number of seconds a resolver may cache a record before querying again. If the challenge says “for all of the DNS records,” it usually means each answer record in that response has the same TTL value, so you read that value from the answer records. 3600
5.	What is the IP address for the “welcome” subdomain?
ANS: In the Answers section, look for the record whose name is the welcome subdomain. Then read its returned IP address. If the query type is A, that will be an IPv4 address. 1.1.1.1
