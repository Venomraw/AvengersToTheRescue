# Crypto / Cipher

## CyberChef Local Install 

option 1: using docker 
```
docker pull ghcr.io/gchq/cyberchef:latest
docker run -p 8000:8000 ghcr.io/gchq/cyberchef:latest
```
open:
```
http://localhost:8000
```
option 2: local build

```
git clone https://github.com/gchq/CyberChef.git
cd CyberChef
npm install
npm start
```
## CyberChef  Notes
CyberChef layout

- Left panel: operations
- Recipe: pipeline (order matters)
- Right panel: live output
- "Magic" is useful but fallible

process 
1. Paste ciphertext
2. Try Magic
3. Identify charset
    1. A–Z only → substitution / shift
    2. Base64 charset → decode
    3. Hex → decode
4. Try ROT / Caesar
5. Try Vigenère (with guessed keys)
6. Try XOR (single byte first)

## Quipqiup Notes

- Online only: https://quipqiup.com
- Paste cipher → Substitution
- Let solver run, then tweak manually
- Lock correct letters early

Use when

- Monoalphabetic substitution
- English‑like spacing
- No obvious encoding layer

## Shift Ciphers

Indicators

- Only letters, single case
- Frequency resembles natural language
- Small shifts reveal readable text

search for ROT13 on CyberChef after pasting in the ciphertext (ex: iveghny ynxr ) 

or on the command line
```
for i in {1..25}; do
echo "SHIFT $i"
caesar $i "ciphertext"
done
```
replace "ciphertext" with the actual ciphertext and look for somthing readable 

## Language‑Specific Ciphers

in CyberChef use frequency distribution to see the common letters for a spiffic language  
then ues the vigenère cipher with a key 

(ex: Y ln xkv lubj swlzqvkht, A vmzb pjk bbua we ddgs ILQ-GQYU-8026)  
using the key: qizkwcgqbs  

or on the command line

`langdetect <<< "ciphertext"`

replace "ciphertext" with the actual ciphertext and this outputs the language (ex: fr)  
 `langdetect` is a part of Python package so you need Python installed

## Strings

Purpose is to extract readable text from binaries or files

use `strings` with `grep` on the command line to search for text  
with the file (ex: Steg1.jpg)  

`strings Steg1.jpg | grep SKY`

use for 

- Hidden flags in executables
- Obfuscated scripts
- Encrypted blobs with plaintext headers

## Atbash Cipher

in CyberChef use search for atbash  
there are no paramiters needed 


or on the command line  
`echo "CIPHERTEXT" | tr 'abcdefghijklmnopqrstuvwxyz' 'zyxwvutsrqponmlkjihgfedcba'`  
where tr is traslate here it is traslating the letter a with the letter z etc

## Fencing Cipher

Indicators

- Same characters, reordered
- Words feel scrambled
- Hints like "fence", "zigzag", "rails"
  
CyberChef

- Rail Fence Cipher
- Try rails 2–6
- Try both encode/decode

or on the command line
```
python3 - << 'EOF'
from pycipher import Railfence
print(Railfence(3).decipher("CIPHERTEXT"))
EOF
```









