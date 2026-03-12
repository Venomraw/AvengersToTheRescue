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

## Load the TLS Key Log

Go to:

`Edit → Preferences` 

`Protocols → TLS`

(Older Wireshark versions call it SSL)

You will see:

(Pre)-Master-Secret log filename

Click Browse and select the .log file (`sslkeylog.log`)

At this exact moment Wireshark silently decrypts the entire capture

## Identify the Server Hello

The cipher suite chosen by the server is found in the Server Hello message during the TLS handshake

In the filter bar, type:

`tls.handshake.type == 2`

Select the Server Hello packet

In the middle pane, expand:

## Finding the Flag 

Right‑click it on any packet that says HTTP 

and choose `Follow → TLS Stream`

This window is the decrypted website content

- Not packets
- Not metadata

Actual plaintext data the browser saw

Answer
```
1. TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
2. tomsvacations.com
3. SKY-LADN-1435
```


