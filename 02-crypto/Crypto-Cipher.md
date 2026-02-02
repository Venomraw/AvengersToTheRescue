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
### CyberChef  Notes
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

