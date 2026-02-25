# Decrypt

The S in HTTPS stands for secure and it uses the TLS/SSL protocol to achieve its security


Wireshark take the `sslkeylog.log` and turn the network traffic in to HTTP

Without the log, HTTPS cannot realistically be decrypted
With the log → HTTPS becomes plaintext

## Open the capture

Open Wireshark

Then:

`File → Open → SSL Decrypt.pcapng`

Right now everything will still look encrypted
