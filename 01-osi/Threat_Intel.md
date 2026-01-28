## Threat Intel

---

##  NIST & the National Vulnerability Database (NVD)

The **National Vulnerability Database (NVD)** is maintained by **National Institute of Standards and Technology (NIST) ** and is the primary source for U.S. government vulnerability data. It contains:

* CVEs (vulnerability identifiers)
* CPEs (affected products)
* CVSS (Common Vulnerability Scoring System)

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
## 3. CVEs

A **CVE (Common Vulnerabilities and Exposures)** ID uniquely identifies a public vulnerability.

Format:

```
CVE-YYYY-NNNNN
```

Example:

* **CVE-2014-3566** – POODLE (SSL 3.0)

CVEs in NVD include descriptions, severity scores, and affected CPEs.

---
