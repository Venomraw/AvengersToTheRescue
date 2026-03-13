# 🛡️ AWS Instance Metadata Service (IMDS) Pentesting Notes

## 📌 Overview
This challenge demonstrates how to perform **Service Discovery** and **Information Enumeration** against an AWS EC2 Instance Metadata Service.

---

## 🛠️ Key Methodology
The IMDS is a basic HTTP server available at a predictable local address (traditionally `169.254.169.254`). By querying specific paths, you can leak sensitive configuration data.

### 🔍 Discovery & Intuition
* **Root Check:** Navigating to the base URL returns `latest`.
* **Path Traversal:** Appending the returned text (e.g., `/latest/meta-data/`) reveals more sub-directories.
* **Stealth Note:** Use `curl` or a browser instead of `nmap` to avoid triggering **SOC (Security Operations Center)** alarms.

---

## 📊 Challenge Findings & Solutions

| Category | Endpoint Path (after `/latest/meta-data/`) | Result |
| :--- | :--- | :--- |
| **Availability Zone** | `placement/availability-zone` | `us-west-2a` |
| **IAM Role Name** | `iam/security-credentials/` | `liber8-role` |
| **Instance Type** | `instance-type` | `c6g.16xlarge` |
| **OS / AMI Name** | `ami-id` (Lookup via Ubuntu Locator) | `Xenial Xerus` |
| **The Flag** | `network/interfaces/macs/[MAC]/vpc-ipv4-cidr-blocks` | `SKY-AWSM-1570` |

---

## 💡 Technical Deep-Dive

### 1. Identifying the OS
The `ami-id` endpoint returns a string like `ami-08305...`. To identify the actual Operating System:
1. Retrieve the ID.
2. Search the [Ubuntu EC2 Locator](https://cloud-images.ubuntu.com/locator/ec2/).
3. **Result:** Ubuntu 16.04, codenamed **Xenial Xerus**.

### 2. Deep Enumeration (The Flag)
To find the hidden flag, you must follow the trail of MAC addresses:
1. Access `.../network/interfaces/macs/`.
2. This returns a MAC address (e.g., `06:1a...`).
3. Append that MAC to the URL: `.../macs/06:1a.../`.
4. Enumerate all sub-paths until reaching `vpc-ipv4-cidr-blocks`.

---

## ⚠️ Security Implications
> [!IMPORTANT]
> Accessing `iam/security-credentials/` is a high-priority target for attackers. In a real-world scenario, this endpoint can leak **Access Keys**, **Secret Keys**, and **Session Tokens**, allowing an attacker to take over the entire cloud environment.

---

## 🔗 Useful Resources
* [AWS Official Metadata Categories](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instancedata-data-categories.html)
* [Ubuntu Cloud Image Locator](https://cloud-images.ubuntu.com/locator/ec2/)
