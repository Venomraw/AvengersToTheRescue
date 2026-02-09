Notes on Data and Encoding

Data refers to any information that is gathered or retained for the purposes of use, measurement, or processing.

It may encompass numerical data, textual content, photos, audio files, video recordings, sensor measurements, and more.

Examples of data:

- 23 (a temperature)
- "Kashish" (a name)
- a photo file
- a list of quiz scores

Encoding

Encoding is the process of converting data into a specified format for storage, transmission, or comprehension by a computer or system.  
In other terms, data constitutes the information; encoding refers to the method of transcribing that information.

Examples of encoding:

- Text stored as ASCII or UTF-8
- A photo saved as JPEG or PNG
- Audio saved as MP3 or WAV
- Numbers represented in binary (0s and 1s)

Tools used for data and encoding

A. CyberChef: It is an online tool used for encoding/ decoding for number bases and strings conversions, hec/ASCII. It is also used for crypto experiments.

How to use CyberChef:

 1. Insert or upload your input into the Input section (left panel)
 2.  Construct a recipe by maneuvering operations into the central area (e.g., "From Hex", "To Base64", "To ASCII", etc.).
   3. Observe the output refresh in real-time.
  4.  Utilize Magic (auto-detect) if the encoding is uncertain.
  5.  Adjust operational parameters (such as charset, endian, etc.) if the output appears incorrect.

B. Rumkin: It is basically the set of classic cipher tools that includes atbash, rail Fence, Caesar /shift.

How to use Rumpkin
 1. Choose the cipher tool you need (e.g., Caesar/Shift, Atbash, Rail Fence).
2.  Paste ciphertext/plaintext
3. Enter the key/shift/rails if required.
4.  Click the encode or decode.

C. Quipquip: It is an is an automated solution for substitution ciphers, in which each letter is regularly replaced by another letter.

How to use:

1.  Paste the ciphertext into the box.
2.  Let it generate guesses
3. Use hints/known words (called **cribs**) if it has that option.
4. Keep refining until the output looks like real language.

Gym Challenges

Number bases

- Used [RapidTables](https://www.rapidtables.com/convert/number/hex-to-ascii.html) to convert the given encoded text. ANS: scorpion
- Used [CyberChef](https://cyberchef.cyberskyline.com/#recipe=From_Base64%28'A-Za-z0-9%2B/%3D',true,false%29) to convert the given encoded text. ANS: scribble
- Used [Binary Hex Converter](https://www.binaryhexconverter.com/binary-to-ascii-text-converter) to convert the given encoded text. ANS securely
- Used [Binary Hex Converter](https://www.binaryhexconverter.com/binary-to-ascii-text-converter) to convert the given binary to ASCII text value then further decoded using [Base64Decode](https://www.base64decode.org/).

Shift

- Used [Rot13](https://rot13.com/) to decode the given text. ANS: virtual lake

Bash

- Used [Rumkin](https://rumkin.com/tools/cipher/atbash/) to decode the given text. ANS: safely obvious cave

Beep

- Used the [Morse Code Translator](https://morsecode.world/international/translator.html) for decoding the given text. ANS: THE SECRET OF GETTING AHEAD IS GETTING STARTED SKY DKVB 981N

Classifying the given encoded texts:

- If the given data looks like structured data/encoding, use CyberChef first.
- The common clues on the data could be letters or numbers with +, / and often ends in =. Use the Base64 decode.
- **Hex**: only 0-9 a-f (often in pairs), may have spaces or 0x. Use Cyberchef, choose "From Hex"
- Any data that includes 0 or 1 Use Cyberchef "From Binary"
- Any URL encodings include %20, %3D. Use the Cyberchef "URL Decode"

Somethings to remember.

\*\*\*If it's about data/encoding/bases and strings." Begin with CyberChef. It is most reliable. \*\*\*\*

- Is it mostly numbers/symbols (base64/hex/binary/url)? Use: CyberChef
- Is it readable letters but nonsense + title says Shift/Atbash/Fence? Use: Rumkin
- Is it sentence-like with punctuation, but letters are swapped Use: Quipquip
- Is it a fixed-length random string (hash)? Use: hashID, then cracking tool (authorized only)