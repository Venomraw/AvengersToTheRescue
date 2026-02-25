# Telnet

Telnet is an older remote‑administration protocol that allows a user to log into another computer 
over the network Unlike modern protocols such as SSH, Telnet does not encrypt traffic, meaning usernames, 
commands, and system information can be recovered directly from a packet capture

First open Wireshark and loaded the provided capture file:  
`File → Open → Telnet.pcap`

Since I only wanted to see Telnet traffic, I applied a display filter:

`telnet`

This removes all unrelated packets and showed only the Telnet session

## Following the TCP Stream

Steps:

Right‑click any Telnet packet

Click Follow → TCP Stream

This reconstructs the entire login session exactly as it appeared to the user and the server

## Finding the Username

Telnet echoes what the user types.
Wireshark color‑codes the conversation:

Blue text = what the user typed
Red text = what the server responded

## Finding the Password

After the username, the server prompts:

`Password`

Unlike the username, the password is not echoed to the screen, so you will not see it typed out normally

Telnet is unencrypted, the password is still present in the TCP stream — it just appears as characters sent without 
being displayed by the server. By carefully looking at the raw stream data between the password prompt and the successful login message, 
the password can be recovered.

## Determining the Hostname

The hostname can be identified in two possible places:

The command output
The shell prompt

Example format:

hostname login:
hostname $
hostname #

The machine name appearing before the prompt is the hostname.

## Determining the CPU Architecture

The command output also lists system architecture information.

Common values you might see:

| Output   | Meaning              |
|----------|----------------------|
| x86_64   | 64-bit Intel/AMD     |
| i386     | 32-bit Intel         |
| i686     | 32-bit Intel         |
| armv7l   | 32-bit ARM           |
| aarch64  | 64-bit ARM           |

The architecture appears near the end of the system information line.

Answers 
```
1. test 
2. capture	
3. $uname -a
4. 2011
5. cm4116
6. armv4tl
```


