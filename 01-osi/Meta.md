**Prarthana Neupane**

**Notes : META**

Meta is also called as metadata which can simply be explained as data _about_ data. It is the hidden or background information associated with files, images, web pages, and sometimes network artifacts.

 **1. WHO uses Meta?**

- Security operations center analysts (Cops, FBI) or incident responders mostly to learn what created a file, where it came from, or clues about a campaign.
- Threat intel/investigators also use it to connect people, tools, timelines, and locations.
- Journalists/researchers use it to verify the authenticity and context of the information.
- NCL players use this to find flags hidden in EXIF, PDF properties, document author fields, etc.

 **2. WHEN is Meta used?**

- Quick hints before delving deeper, early reconnaissance/triage.
- While investigating, it is used to verify the creation date, software version, device information, and timestamps.
- Checking the authenticity of the file and whether it has been altered in any way.
- Metadata frequently includes step-by-step information such as a name, username, domain, GPS, or software.

 **3. WHERE is metadata available or where can one find the metadata?**
- Images
     EXIF: camera model, date/time, GPS (sometimes), lens, settings
     XMP: editing software, history, creator fields

- Documents

     PDF: author, producer, creation tool, timestamps
    Word/PowerPoint: author/company, last saved by, revision history (sometimes)

- Webpages

    - HTML &lt;meta&gt; tags (description, author, generator)
    - Page source comments
    - OpenGraph/Twitter cards
    - Sometimes hidden values in JS or embedded files

- Network/Web artifacts (NCL sometimes includes this)

     - HTTP headers (server type, caching, framework hints)
     - SSL certificate info (issuer, dates, names) (often a later "SSL" guide, but the idea is still "meta")

**4. HOW is Meta used (practical NCL method)?**
  ANS: Metadata is used by step to step method practically like explained below:

Step 1: Identify the object

- What is it? Image? PDF? Website?  
    Knowing file type tells you what metadata to look for.

Step 2: Extract metadata

- Images: EXIF/XMP fields
- PDF/Docs: document properties fields
- Websites: view source + headers

Step 3: Scan for "high-value fields"  
Look specifically for:

- Author / Creator / Producer
- Software / Editor / Generator
- Create/Modify timestamps
- GPS / Location clues
- Usernames / Paths (sometimes documents leak folder paths)
- Hidden comments/keywords

Step 4: Pivot  
The next search is for any clue you find from early findings or discoveries.

- Author name → username lookup
- Software version → identify tool chain
- Timestamp/timezone → build a timeline
- GPS/city → location context

Step 5: Validate  
Metadata can be stripped, spoofed, and time zoned, which is why validating it is a very important step. So always cross-check with another source.

**Meta Answers**

1\. When was the image created? (Round to the nearest minute)

Ans: 15<sup>th</sup> May 2015 Time : 02:14

2\. What is the image size in pixels? (ex: 800x600)

Ans: 1920\*1440

3\. What is the make of the camera that took the picture?

Ans: Apple Iphone 5

Tools Used

- [Metadata Viewer](https://www.metadata2go.com/)