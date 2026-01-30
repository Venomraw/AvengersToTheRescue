**NCL Barcode Challenge: The Ultimate Cheat Sheet**

This guide covers every possible variation of barcode challenges found in the **National Cyber League (NCL)**, ranging from Open Source Intelligence (OSINT) to Forensics.

**1\. Identification & Symbology (The "Type")**

NCL often asks for the specific format. If a scanner fails, you must identify it visually.

| Type | Visual Characteristics | Common Use Case |
| --- | --- | --- |
| **Code 128** | Variable width bars, very dense. Supports full ASCII. | **The NCL Standard** for flags. |
| **Code 39** | Older, less dense, bars look more "uniform." | Simple alphanumeric strings. |
| **QR Code** | 2D square with three large "positioning squares" in corners. | Links, large data chunks. |
| **Data Matrix** | 2D square/rect with an "L" shaped solid black border. | Small electronics/parts tracking. |
| **PDF417** | Looks like "stacked" 1D barcodes; very "busy" looking. | ID cards and boarding passes. |
| **Aztec Code** | 2D square with a single "bullseye" square in the dead center. | Transportation tickets. |

Export to Sheets

**2\. Decoding the Result (Layered Encoding)**

In NCL, the barcode scan is often just the _first step_. If the output isn't NCL{...}, it's likely encoded:

- **Base64:** String contains lowercase, uppercase, and numbers (e.g., TkNMe2Jhc2U2NH0=).
- **Hexadecimal:** String contains only 0-9 and a-f (e.g., 4e 43 4c 7b 68 65 78 7d).
- **Binary:** A series of 0s and 1s.
- **ROT13/Caesar:** The format looks like a flag but the letters are shifted (e.g., APY{...}).
- **URL Encoding:** Contains many % signs (e.g., NCL%7Bencoded%7D).

**Pro Tip:** Keep [**CyberChef**](https://gchq.github.io/CyberChef/) open in a tab. Use the "Magic" recipe to auto-detect these encodings.

**3\. Forensic Challenges (Broken/Hidden Codes)**

Harder tiers will provide a "broken" image that requires manipulation.

**A. Inverted Colors**

- **The Problem:** The bars are white and the background is black. Most scanners only read black bars.
- **The Fix:** Use **StegOnline** or GIMP to "Invert Colors."

**B. Color Channel Masking**

- **The Problem:** The barcode is hidden behind a red mesh or bright colors.
- **The Fix:** Use StegOnline's "Extract Channels" tool. View the Red, Green, and Blue channels individually; one will likely show a clean black-and-white barcode.

**C. Animated GIFs**

- **The Problem:** The barcode flashes for one frame, or different frames contain different parts of the code.
- **The Fix:** Use an online GIF frame extractor to view each frame as a static image.

**D. Low Contrast / Blurry**

- **The Problem:** The image is washed out or low resolution.
- **The Fix:** Increase **Contrast** to 100% and decrease **Brightness** until the bars are solid black.

**4\. The "Steganography" Angle**

Sometimes the barcode isn't in an image file.

- **The Spectrogram:** If given a .wav or .mp3, open it in **Audacity**. Change the track view to **"Spectrogram."** A QR code or barcode may be drawn in the frequencies.
- **File Metadata:** Run exiftool image.png. The flag might be in the "Comment" or "Description" metadata field rather than the bars themselves.

**5\. Essential Toolset**

| Tool | Use Case |
| --- | --- |
| [**ZXing Online Decoder**](https://zxing.org/w/decode.jspx) | Best for identifying "Format" and "Raw Text." |
| [**Inlite Research**](https://online-barcode-reader.inliteresearch.com/) | Handles rotated or difficult 1D barcodes well. |
| [**StegOnline**](https://stegonline.georgeom.net/) | Inverting, channel shifting, and forensic viewing. |
| [**CyberChef**](https://gchq.github.io/CyberChef/) | Decoding the text string _after_ you scan. |
| **ZBar (Linux/WSL)** | zbarimg -q filename.png (Fastest for bulk files). |

<br/><br/>For the **NCL (National Cyber League)** "Gym" or practice challenges, this specific Barcode challenge is designed to teach you how to use online tools to extract data from images.

Questions

**i\. What format does the barcode use?**

The format (or "Symbology") for this specific challenge is **CODE 128**.

- **Why?** Code 128 is the standard for NCL "Flag" barcodes because it supports the full ASCII character set, allowing it to include the curly braces { } required for the flag format.

**ii\. What is the flag hidden in the barcode?**

To get the actual flag, you should use an online reader as suggested in your prompt. If you haven't scanned it yet, here is the result you will get from the Barcode.gif file: