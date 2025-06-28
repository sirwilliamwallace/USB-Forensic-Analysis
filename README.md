# Digital Forensics Investigation – USB Analysis on Raspberry Pi

## Related Article

I wrote a detailed guide on setting up the Raspberry Pi with Kali Linux and securing it via Tailscale, which was used in this forensic investigation:

**➡️ [How to Install Kali Linux on a Raspberry Pi and Access It Securely (Tailscale Version)](https://medium.com/@mrnumberx/how-to-install-kali-linux-on-a-raspberry-pi-and-access-it-securely-tailscale-version-1a663d64ec74)**  
Published on *Medium* by Amirhossein Shekooh

---

## Overview

This project documents a full **digital forensic analysis** of a suspicious 2GB USB flash drive, conducted as part of a university module in Digital Forensics. Using a **Raspberry Pi 4** configured with **Kali Linux** and remote-secured via **Tailscale**, I followed a professional-grade investigation workflow including evidence imaging, hashing, file carving, and advanced analysis of hidden malicious payloads (ZIP bombs).

---

## Tools & Technologies

- Kali Linux on Raspberry Pi 4 (custom SSH-only setup)
- FTK Imager (image creation + MD5 & SHA-1 verification)
- Foremost (file carving)
- Binwalk & Strings (advanced ZIP analysis)
- Tailscale (secure remote access)

---

## Key Steps

### 1. Write-Blocked Imaging

- USB was imaged using FTK Imager v4.7.3 with a USB write blocker.
- MD5 & SHA-1 hashes were created and verified to ensure integrity.

![image](https://github.com/user-attachments/assets/34afe317-4dc4-40db-ad6b-4f116d270f15)

```plaintext
MD5: 958eaee85ace515af653944635913209
SHA-1: a641ff2f1b66fa37b9605f8aa0cf6a033fd02e06
```
![image](https://github.com/user-attachments/assets/e1e504e7-f992-4ec5-a385-ee44c1a34df1)

### 2. Secure Analysis Environment

- Raspberry Pi 4 running Kali Linux configured with `USER` as sole user.
- Remote SSH access is locked to the examiner's device via Tailscale.

---

### 3. File Carving & Threat Discovery

- Image file `usb-raw-img.dd.001` analysed using Foremost.
- Two ZIP files were carved: both later flagged as corrupted/malicious.
![image](https://github.com/user-attachments/assets/19405016-296d-4782-84b3-6372483d9b9e)
![image](https://github.com/user-attachments/assets/171cf585-b73c-4583-8250-21913b694592)

```bash
foremost -i usb-raw-img.dd.001 -o recovered_files
```
### 4. Safe Static Analysis

- Binwalk, Strings, and Zipinfo were used to examine ZIP files without extracting them.

- Found patterns of repeated JPEGs and text files: indicators of ZIP bombs

![image](https://github.com/user-attachments/assets/bb9b51ad-141b-4203-a73f-da94fbcb0c37)

ZIP info:
![image](https://github.com/user-attachments/assets/a08736cd-db33-416f-9c42-c122ff0c5c7c)

Binwalk:
![image](https://github.com/user-attachments/assets/76543919-149e-4f2f-9451-2d48098ef467)

## Legal & Ethical Considerations
- All actions complied with GDPR, data integrity, and chain-of-custody protocols.

- Confidential or suspicious data was not stored on personal machines.

- Tailscale ensured an isolated forensic analysis environment.

### Key findings
![image](https://github.com/user-attachments/assets/67b473ea-16ce-47d7-a5c4-de250375cbda)

- ZIP bombs were embedded with repetitive, oversized, corrupted files.

- Designed to crash systems or delay forensic work.

- Proper isolation and safe tools mitigated risks successfully.

## Licence
This project is licensed under the MIT License – see the [LICENSE](./LICENSE) file for details.

## Author
**Amirhossein Shekooh**
BSc Cybersecurity
Feel free to explore the report or reach out for discussion or collaboration.
