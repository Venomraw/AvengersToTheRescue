## Threat Intel

---

##  NIST & the National Vulnerability Database (NVD)

The National Vulnerability Database (NVD) is maintained by National Institute of Standards and Technology (NIST) and is the primary source for U.S. government vulnerability data. It contains:

- CVEs (vulnerability identifiers)
- CPEs (affected products)
---
## CPE Lookup (NVD)

CPE (Common Platform Enumeration) is a standardized way to name software and hardware.

Use the NVD CPE Search: https://nvd.nist.gov/products/cpe/search

steps:

- Search for a product and version

- click on the CPE 2.3 string

- click View Vulnerabilities at the bottom to see related CVEs

Example CPE:

```
cpe:2.3:a:openssl:openssl:1.0.2f:*:*:*:*:*:*:*
```
---
## CVEs

A CVE (Common Vulnerabilities and Exposures) ID uniquely identifies a public vulnerability.

Format:

```
CVE-YYYY-NNNNN
```

Example:

* CVE-2014-3566 – POODLE (SSL 3.0)

## Answers for the gym challenge

CVEs in NVD include descriptions, severity scores, and affected CPEs.


1. What is the CVE of the original POODLE attack?

`CVE-2014-3566`

2. What version of VSFTPD contained the smiley face backdoor?

`vsftpd 2.3.4`

3. What was the first 1.0.1 version of OpenSSL that was NOT vulnerable to heartbleed?

`OpenSSL Version 1.0.1g addresses and mitigates this vulnerability`

4. What was the original RFC number that described Telnet?

`RFC 854 and 855`

5 .How large (in bytes) was the SQL Slammer worm?

`376 bytes`

6 .Samy is my…

`Hero`
