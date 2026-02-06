**Prarthana Neupane**

**Notes: LOOKUP**

**"Lookup" (in NCL)**

Using a single piece of data as a "indicator" and searching public databases for more information allows one to conduct a lookup in NCL and perhaps uncover fresh insights.

**1. WHO uses Lookup OSINT?**

When using NCL for a lookup, you take a single piece of data (an "indicator") and use it to query a database.

- SOC/cyber defenders use a lookup for proper enhancement of suspected domains, IP addresses, and emails in the event of an alert.
- Connect infrastructure and spot patterns: that is the job of threat intelligence analysts.
- Teams dealing with fraud and abuse use lookup to verify the sites' or accounts' validity.
- Players in the NCL should properly and swiftly follow breadcrumbs to discover more and switch to fresh clues.

**2. WHEN is Lookup used?**

- Immediately after you find a clue (from Meta, WHOIS, Headers, SSL, etc.)
- During triage ("Is this domain shady?")
- When you need enrichment (owner/org, location, related domains, history)
- When you're stuck and need a new pivot

**3. WHERE do you perform lookups?**

Common public lookup "places" (types of sources):

 a) Domain & DNS

 - WHOIS/registrar data
 - DNS records: A/AAAA, MX, TXT, CNAME, NS
 - Domain history (sometimes)

 b) IP address

- ASN/ISP/org ownership
- Geolocation (approximate)
-  Reverse DNS (PTR)
- Reputation context (if available)

 c) Identity strings

 - Username handles
 - Email addresses _(only ethically-prefer your own or provided/authorized targets)_
 - Phone numbers _(same-don't use to stalk or dox)_

d) Website footprint

- "About/Contact" pages
- Social links
- Cached/archived versions (the web archive idea)

**4.HOW is Lookup used (the NCL way)?**

Use this "pivot ladder":

Step 1: Start with one indicator  
Examples:

- domain: example.com
- IP: 1.2.3.4
- username: coolhandle
- email: <name@domain.com>

Step 2: Pick the correct lookup type

- Domain → WHOIS + DNS
- IP → ASN/org + geolocation
- Username → platform search + consistency checks

Step 3: Record what you learn (like a mini evidence log)  
Write down:

- Source used
- Exact result (org/name/date)
- Confidence level (high/medium/low)

Step 4: Pivot from results  
Examples of pivots:

- WHOIS org name → search org + domain connections
- DNS TXT record → might reveal services or verification strings
- IP ASN → find other domains hosted nearby (sometimes)
- Username → find same handle on other platforms (pattern matching)

Step 5: Cross-check  
Never trust one lookup alone:

- WHOIS may be privacy-protected
- GeoIP can be inaccurate
- Usernames can be reused by different people

"Lookup" in NCL usually tests skills like:

- Choosing the right lookup tool/source for the clue
- Reading results correctly (registrar vs registrant vs name server)
- Identifying what's useful vs noise
- Pivoting logically (one clue to next clue)
- Not making wild assumptions

**Lookup Answers**

- What type of DNS record holds the DNSSEC public signing key?

ANS: DNSKEY record (holds the DNSSEC public signing key)

- What type of DNS record is used to map hostnames to IPv6 addresses?

ANS: AAAA record (maps hostnames to IPv6 addresses)

- What type of DNS record is used to delegate a DNS zone?

ANS: NS record (delegates a DNS zone by listing authoritative name servers)

- Sources for Lookup answers: [RFC 4034](https://datatracker.ietf.org/doc/html/rfc4034), [RFC 3596,](https://www.rfc-editor.org/rfc/rfc3596) [RFC 1035](https://tools.ietf.org/html/rfc1035).