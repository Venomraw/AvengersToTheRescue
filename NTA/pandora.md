**1️⃣ Protocol Specification Breakdown**

Before analyzing the PCAP file, understand the protocol structure.

**All integers are in Network Byte Order (Big Endian).**

**📦 Message Structure**

| **Message Type** | **Sender** | **Field** | **Size** | **Description** |
| --- | --- | --- | --- | --- |
| Initialization | Client | N | 4 Bytes | Number of Hash Requests to follow |
| Pre-Response | Server | Len | 4 Bytes | Total length of the upcoming Hash Response |
| Hash Request | Client | Check | 2 Bytes | Integrity/Magic Number (look for 0x0417) |
|  |  | Len | 4 Bytes | Length of the Data field |
|  |  | Data | Variable | The actual payload to be hashed |
| Hash Response | Server | Count | 4 Bytes | Length of the following hashes |
|  |  | Hashes | Variable | Concatenated hashes (fixed length per hash) |

**2️⃣ Wireshark Workflow**

To analyze efficiently, remove unnecessary traffic and focus on raw byte data.

**🔎 Step 1: Filter Traffic**

The capture includes SSH (port 22) and HTTP (port 80).
Use this display filter to isolate the Pandora protocol:

tcp && !(tcp.port == 22) && !(tcp.port == 80)

**🔍 Step 2: Follow the TCP Stream**

1. Right-click the first packet in the filtered results.
2. Select:

Follow > TCP Stream

1. Change **"Show data as"** to:

Hex Dump

⚠️ This is critical — custom protocols are often non-ASCII.

**3️⃣ Byte-Level Analysis (The "Math")**

**🧩 Identifying the Magic Number**

The **Check value** is:

0x0417

Use this value as a bookmark to locate where each new **Hash Request** begins in the hex dump.

**🧮 Calculating Hash Length**

If:

* Server total response length = 160 bytes (0xa0)
* Number of requests = 5

Then:

160 ÷ 5 = 32 bytes per hash

✅ A 32-byte hash (256 bits) strongly suggests:

SHA-256

**4️⃣ Finding the Flag 🚩**

The shortcut:
The flag is hidden inside the **Data portion of the Hash Requests** sent by the client.

**🔍 Steps:**

1. Locate the **Data field**:
   * After:
     + 2-byte Check
     + 4-byte Len
2. Examine the data:
   * If it looks like:

SGVsbG8=

It is likely **Base64 encoded**.

1. Action:
   * Copy the Data field
   * Use **CyberChef**
   * Apply:

From Base64

🎉 This should reveal the flag.

**5️⃣ Summary of Key Values (This PCAP)**

| **Parameter** | **Value** |
| --- | --- |
| Number of Requests (N) | 5 |
| Magic Check Value | 0x0417 |
| Request 1 Data Length | 88 bytes (0x58) |
| Request 2 Data Length | 72 bytes (0x48) |
| Single Hash Length | 32 bytes |