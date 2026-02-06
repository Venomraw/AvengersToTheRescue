# WHOIS

WHOIS is a protocol for querying databases that store information about internet resources and domain names. For domain names, instead of using IP addresses usually consisting of numbers for example 192.168.1.102, a domain name like google.com is used instead allowing easier identification and access.

## Function of WHOIS

How WHOIS works is it utlizes a TCP port 43 and when a request is sent to the server, it respond back with information that is readable.

## Why is it created?

The reason for WHOIS creation is for:
- Manage domain name registrations
- Checking domain availability
- Making sure the DNS is functioning smoothly
- Tracking and verfiying domain ownershio
- Storing contact information
 
## ICANN

ICAAN has a tool which is a registration data lookup, which can allow you to find domains and Internet number resources that are currently register. It can be found on the [ICANN Lookup website](https://lookup.icann.org/en)

Information you can find you when entering in a domain name or Internet number resource are:
- Domain Information
- Contact Information
- Registrat Information
- DNSSEC Information
- Authoriatative Servers
- Notice and Remarks


## Performing a WHOIS lookup

There are a few ways to perform a lookup using WHOIS:

1. Linux Terminal
    - Install sudo apt install whois(If not installed)
    - Enter the command `whois google.com`(Any working domain name)
    - Review the information

- Lookup Tool like [ICANN Lookup](https://lookup.icann.org/en)
    - Go to the lookuptool website
    - Enter domain name in the search bar for example google.com
    - Review the information

### Gym challenge answers
 1. Who is the registrar of this domain?

    The registrar is Dynadot Inc

 2. On what day this domain first registered?
    
    It was created on 2016-02-16 

 3. What is this domain's registry domain ID?

    Thie id is D15CD1AC4DEB54207A5048A69B9FC0558-ARI