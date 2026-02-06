# HTTP Headers and SSL

This document will contain notes and answers found in the [HTTP Headers](https://trove.cyberskyline.com/0d6e926b2e5b402bacdd6b62cb48e342) and the [SSL](https://trove.cyberskyline.com/8835d44ab9914ab98e25c6b2b5999abf) pages found in the NCL Resources Guide.

---

## HTTP Headers

1. URL

    URLs (Uniform Resource Locators) are used to specify the location of a resource on the internet. URLs usually include the following with examples.
    - A protocol (`https://www.`)
    - A domain name (`google.com`)
    - An optional path (a `/` after `.com`)

2. URI

    URIs (Uniform Resourse Identifier) help find the location of a resource on the internet after a user enters a URL.

3. Protocols

    Protocols define the rules and formats for networked devices. This usually comes in the form of HTTP and HTTPS.

4. GET, POST, and FTP Equivalents

    - GET requests data from the server. This is usually used go load websites.
    - POST sends data to the server. This is used for making a post on social media for example.
    - FTP is used for file transfer. This is usually used for downloading files onto a computer.

### Answers for the gym challenge

1. What HTTP request header is used to denote what URI linked to the resource being requested?
    
    The request is called `Referer`.

2. What HTTP request header is used to identify the client software that made the HTTP request?

    The request is called `User-Agent`.

3. What HTTP request header is used to identify the acceptable content types that can be returned?

    The request is called `Accept`.

---

## SSL

SSL (Secure Sockets Layer) is a security protocol and encrypts traffic so you can use HTTP securely. SSL is also used (or at least was used) in the HTTPS protocol.

1. SSL Certificate Chains

    An SSL chain is used to verify the authenticity of a server using multiple certificates. These certificates include the following in order of how a chain works and explanations on what each certificate does.

    - A root certificate. This what validates the intermediate certificate(s) and appoves a connection.

    - An intermediate certificate. This is what is used between the root and server certificates. This is what is used to link the two certificates together. (The chain can include multiple intermediate certificates)

    - A server certificate. Identifies websites and establishes an encrypted connection.

2. Certificate Authority and Trust

    Certificate Authority (CA) is what issues certificates. Trust is established when a client recognizes the CA from its issuer.

### Answers for the gym challenge

1. Who is the issuer for Cyber Skyline's SSL certificate?

    The issuer is R13.

2. How many bits long is the SSL key?

    2048 bits.

3. How many certificates are in the certificate chain?

    There is only 1 certificate.