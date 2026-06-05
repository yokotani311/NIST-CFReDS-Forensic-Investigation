# NIST CFReDS Hacking Case – Digital Forensic Investigation Report

## Overview

This repository contains a digital forensic investigation report based on the official **NIST CFReDS Hacking Case** disk image.  
The investigation was conducted as part of a hands-on forensic analysis exercise at **Douglas College** (Post-Baccalaureate Diploma in Computer and Information Systems).

The report demonstrates the ability to:
- Acquire and verify forensic evidence images
- Analyze Windows registry artifacts and user activity
- Reconstruct a timeline of suspicious activities
- Document findings in a format suitable for legal proceedings

---

## Case Summary

| Item | Details |
|------|---------|
| Case | NIST CFReDS – Hacking Case |
| Target Device | Dell Latitude CPi (sn#: VLQLW) |
| Acquisition Date | September 22, 2004 |
| Examiner (Original) | Shane Robinson |
| File Format | EnCase 4 (E01) |
| MD5 Hash | aee4fcd9301c03b3b054623ca261959a |
| OS | Windows XP |

---

## Tools Used

| Tool | Purpose |
|------|---------|
| `ewfinfo` | Evidence image metadata extraction |
| `mmls` | Partition structure analysis |
| `fsstat` | File system information |
| `regripper` | Windows registry artifact analysis |
| `dd` | Disk imaging and file carving |
| `mmls` | Partition recovery |
| `xxd` | File header / footer extraction |
| `samparse` | User account analysis |
| `Autopsy / FTK Imager` | Evidence image mounting and analysis |

---

## Investigation Process

### 1. Evidence Verification
- MD5 hash validation to confirm evidence integrity
- Partition structure analysis using `mmls` and `fsstat`
- File system identification (NTFS)

### 2. System Analysis
- Operating system version identification via registry (`winver` plugin)
- User account enumeration using `samparse`
- Identified 5 accounts; primary suspect: **"Mr. Evil"** (Administrator privileges)

### 3. Registry Artifact Analysis
The following `regripper` plugins were applied to extract user activity:

| Plugin | Artifact | Finding |
|--------|---------|---------|
| `uninstall` | Installed software | 8 hacking-related tools identified |
| `recentdocs` | Recently accessed files | keys.txt, channels.txt, Receipt.rtf |
| `typedurls` | Browser URL history | Hacker sites (2600.org, wardriving.com) |
| `usb` | USB device history | External device connected on 2004-08-27 |
| `userassist` | Program execution history | Cain, Ethereal, NetStumbler executed |
| `shimcache` | File existence records | Malicious tools confirmed present |
| `runmru` | Run dialog history | Telnet used for remote access |
| `comdlg32` | File open/save history | Tools launched from Desktop |

### 4. Timeline Reconstruction

| Date | Activity |
|------|---------|
| 2004-08-19 | System setup; USB hub first recognized |
| 2004-08-20 | Installation of Cain & Abel, mIRC, Anonymizer |
| 2004-08-25 | Installation of Look@LAN; network scanning begins |
| 2004-08-27 | NetStumbler, WinPcap, Ethereal installed and executed in rapid succession; USB device connected; FTP access to 4.12.220.254 |

---

## Key Findings

### Suspected Malicious Activities

**Network Reconnaissance**
- Packet sniffing via Ethereal/WinPcap
- Wireless network scanning via NetStumbler
- FTP connection to external server (4.12.220.254) suggesting data exfiltration

**Credential Theft**
- Password hash cracking via Cain & Abel
- Sensitive files: `keys.txt`, `Receipt.rtf`

**Evidence Concealment**
- Anonymizer tools used to obscure browsing activity
- Use of Temp folders to hide files

---

## Conclusion

Based on registry artifacts, execution history, and timeline analysis, it is concluded that the user **"Mr. Evil"** was engaged in a deliberate and systematic network intrusion campaign between August 19–27, 2004.  
The findings are documented in a format consistent with forensic reporting standards suitable for legal proceedings.

---

## Report

📄 [View Full Investigation Report (PDF)](./NIST-CFReDS-Hacking-Case-Report.pdf)

---

## About the Author

**Yoko Tani**  
Post-Baccalaureate Diploma in Computer and Information Systems  
Douglas College, Vancouver, Canada (2026)  
GPA: 4.16 / 4.33

**Technical Skills:** Digital Forensics (FTK Imager, Autopsy, regripper, dd) | SIEM / Log Analysis (Splunk, Security Onion) | Network Monitoring (Wireshark, tcpdump) | Vulnerability Assessment (Nmap, OpenVAS) | Cloud Security (GCP) | Scripting (Bash, PowerShell, Python)

**Competitions:** NCC CTF – 7th Place (Western Canada Regional) | CyberSci – 9th Place (Vancouver Region)

---

## Disclaimer

This investigation was conducted solely for educational purposes using publicly available forensic disk images provided by the National Institute of Standards and Technology (NIST) CFReDS project.  
Source: https://cfreds.nist.gov
