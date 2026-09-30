# 🏆 OverTheWire: Bandit Wargame — Comprehensive Writeup & Security Guide

<div align="center">

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Bash](https://img.shields.io/badge/Shell_Scripting-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Security](https://img.shields.io/badge/Cyber_Security-E02424?style=for-the-badge&logo=kalilinux&logoColor=white)
![Status](https://img.shields.io/badge/Progress-Level_27%2F34-success?style=for-the-badge)

A complete, highly detailed collection of technical writeups, penetration testing notes, and command-line forensics from solving the **[OverTheWire: Bandit](https://overthewire.org/wargames/bandit/)** wargame.

**[English](README.md)** • **[🇻🇳 Tiếng Việt (Vietnamese Writeup)](README.vi.md)**

</div>

---

## 🌐 Connection Information

All challenges are hosted on OverTheWire's remote infrastructure:

| Parameter | Value |
|:---|:---|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Protocol** | SSH (Secure Shell) |
| **SSH Command Format** | `ssh bandit<N>@bandit.labs.overthewire.org -p 2220` |

---

## 📋 Comprehensive Level Summary & Credentials Matrix

| Level | Current User | Next Password / Access Token | Core Vulnerability / Technique | Detailed Writeup |
|:---:|:---|:---|:---|:---:|
| **0 ➜ 1** | `bandit0` | `6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR` | Remote SSH login & reading files (`cat`) | [📖 Writeup](level_00_to_01.md) |
| **1 ➜ 2** | `bandit1` | `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB` | Dashed filename argument collision (`cat ./-`) | [📖 Writeup](level_01_to_02.md) |
| **2 ➜ 3** | `bandit2` | `7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME` | Shell word splitting & whitespace escaping | [📖 Writeup](level_02_to_03.md) |
| **3 ➜ 4** | `bandit3` | `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq` | Uncovering hidden dotfiles (`ls -la`) | [📖 Writeup](level_03_to_04.md) |
| **4 ➜ 5** | `bandit4` | `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG` | MIME type & magic byte detection (`file ./*`) | [📖 Writeup](level_04_to_05.md) |
| **5 ➜ 6** | `bandit5` | `pXa26xhMWaC2SvDotA4r9EgZkulOeSBW` | Advanced `find` with byte size & inverted flags | [📖 Writeup](level_05_to_06.md) |
| **6 ➜ 7** | `bandit6` | `Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3` | System-wide search with `STDERR` suppression | [📖 Writeup](level_06_to_07.md) |
| **7 ➜ 8** | `bandit7` | `VR1ljMayciFxbnUokuQmJFw6QC9VKtub` | Pattern matching in big data (`grep`) | [📖 Writeup](level_07_to_08.md) |
| **8 ➜ 9** | `bandit8` | `EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl` | Data pipeline sorting & deduplication (`uniq -u`) | [📖 Writeup](level_08_to_09.md) |
| **9 ➜ 10** | `bandit9` | `B0s2khmbT9u0geKuOoVGW3JZKhndE3BG` | Binary string extraction (`strings`) | [📖 Writeup](level_09_to_10.md) |
| **10 ➜ 11** | `bandit10` | `pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro` | Base64 binary-to-text decoding (`base64 -d`) | [📖 Writeup](level_10_to_11.md) |
| **11 ➜ 12** | `bandit11` | `GROozWPO8QyN0mGrjUkID0WCYkZiQxrN` | ROT13 substitution cipher reversal (`tr`) | [📖 Writeup](level_11_to_12.md) |
| **12 ➜ 13** | `bandit12` | `qQYQiHOBPR8zR61qxYqX45quvihF2uzk` | Hexdump reversal (`xxd -r`) & 9-layer decompression | [📖 Writeup](level_12_to_13.md) |
| **13 ➜ 14** | `bandit13` | `aaWecNkG4FhxJQxz07uiwzVP6bJiYS65` | SSH asymmetric private key authentication | [📖 Writeup](level_13_to_14.md) |
| **14 ➜ 15** | `bandit14` | `pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7` | Raw TCP socket communication (`nc localhost`) | [📖 Writeup](level_14_to_15.md) |
| **15 ➜ 16** | `bandit15` | `kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V` | Encrypted SSL/TLS client stream (`openssl s_client`) | [📖 Writeup](level_15_to_16.md) |
| **16 ➜ 17** | `bandit16` | `SSH Private Key (bandit17.key)` | Port scanning (`nmap`) & SSL key extraction | [📖 Writeup](level_16_to_17.md) |
| **17 ➜ 18** | `bandit17` | `OQxXZjELndr90zuhOTDYBEomI0SZITXI` | File differential analysis (`diff`) | [📖 Writeup](level_17_to_18.md) |
| **18 ➜ 19** | `bandit18` | `KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI` | Bypassing `.bashrc` logout with non-interactive SSH | [📖 Writeup](level_18_to_19.md) |
| **19 ➜ 20** | `bandit19` | `4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA` | Local SUID binary privilege escalation | [📖 Writeup](level_19_to_20.md) |
| **20 ➜ 21** | `bandit20` | `bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY` | Background socket listener (`&`) & SUID handshake | [📖 Writeup](level_20_to_21.md) |
| **21 ➜ 22** | `bandit21` | `RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz` | Scheduled task enumeration (`/etc/cron.d/`) | [📖 Writeup](level_21_to_22.md) |
| **22 ➜ 23** | `bandit22` | `gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw` | Reversing dynamic MD5 hash algorithms in scripts | [📖 Writeup](level_22_to_23.md) |
| **23 ➜ 24** | `bandit23` | `hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv` | Cron spool directory shell script injection | [📖 Writeup](level_23_to_24.md) |
| **24 ➜ 25** | `bandit24` | `SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P` | Automated 10,000 PIN brute-force via Bash pipeline | [📖 Writeup](level_24_to_25.md) |
| **25 ➜ 26** | `bandit25` | `jHdv2ELQhT22BkprMNDjybZDAkw1zeBJ` | Restricted shell breakout (`more` ➜ `vi` breakout) | [📖 Writeup](level_25_to_26.md) |
| **26 ➜ 27** | `bandit26` | `*(In Progress / Pending)*` | Interactive shell breakout & SUID execution | [📖 Writeup](level_26_to_27.md) |

---

## 🗂️ Knowledge Domain Taxonomy

```
OverTheWire Bandit Wargame
├── 🐧 Linux CLI & File System Basics (Levels 0 - 9)
│   ├── SSH fundamentals & standard I/O (Levels 0 - 1)
│   ├── Shell parsing, dashes, spaces & dotfiles (Levels 1 - 3)
│   ├── Magic bytes & file type discrimination (Level 4)
│   ├── Advanced `find` queries & error suppression (Levels 5 - 6)
│   └── Stream pattern matching, sorting & binary forensics (Levels 7 - 9)
│
├── 🔐 Cryptography, Encoding & Archives (Levels 10 - 13)
│   ├── Base64 encoding/decoding (Level 10)
│   ├── Classical substitution ciphers / ROT13 (Level 11)
│   ├── Hexdump reconstruction & recursive archive decompression (Level 12)
│   └── Asymmetric SSH key pair authentication (Level 13)
│
├── 🌐 Network Sockets & Transport Security (Levels 14 - 17)
│   ├── Raw TCP stream interaction with Netcat (Level 14)
│   ├── SSL/TLS encrypted transport streams (Level 15)
│   ├── Network service enumeration with Nmap (Level 16)
│   └── Line-by-line file difference analysis (Level 17)
│
├── ⚙️ Privilege Escalation & Linux Automation (Levels 18 - 24)
│   ├── Non-interactive execution bypassing startup scripts (Level 18)
│   ├── SUID binary privilege escalation (Levels 19 - 20)
│   ├── Cron daemon scheduling & path inspection (Level 21)
│   ├── Dynamic MD5 hash reconstruction (Level 22)
│   └── Cron spool script injection exploitation (Level 23)
│
└── 🛡️ Brute-Forcing & Restricted Shell Escapes (Levels 24 - 26+)
    ├── Multi-stream socket brute-forcing (Level 24)
    └── Terminal resizing & Pager/Editor jailbreaks (`more` ➜ `vi`) (Levels 25 - 26)
```

---

## 🚀 Repository Structure

```text
bandit/
├── README.md               # Summary hub and credentials matrix
├── level_00_to_01.md       # Level 0 -> 1: SSH connection & file reading
├── level_01_to_02.md       # Level 1 -> 2: Dashed filename handling
├── level_02_to_03.md       # Level 2 -> 3: Whitespace handling in filenames
├── level_03_to_04.md       # Level 3 -> 4: Hidden files inspection
├── level_04_to_05.md       # Level 4 -> 5: Human-readable file detection
├── level_05_to_06.md       # Level 5 -> 6: Finding files by byte size
├── level_06_to_07.md       # Level 6 -> 7: System-wide search with permissions
├── level_07_to_08.md       # Level 7 -> 8: Grepping keywords in data files
├── level_08_to_09.md       # Level 8 -> 9: Unique line filtering with sort/uniq
├── level_09_to_10.md       # Level 9 -> 10: Extracting strings from binary
├── level_10_to_11.md       # Level 10 -> 11: Base64 decoding
├── level_11_to_12.md       # Level 11 -> 12: ROT13 cipher rotation
├── level_12_to_13.md       # Level 12 -> 13: Hexdump & recursive archive extraction
├── level_13_to_14.md       # Level 13 -> 14: SSH private key authentication
├── level_14_to_15.md       # Level 14 -> 15: Netcat TCP socket interaction
├── level_15_to_16.md       # Level 15 -> 16: SSL/TLS client with OpenSSL
├── level_16_to_17.md       # Level 16 -> 17: Nmap scanning & SSL key capture
├── level_17_to_18.md       # Level 17 -> 18: File diff comparison
├── level_18_to_19.md       # Level 18 -> 19: Bypassing .bashrc logout
├── level_19_to_20.md       # Level 19 -> 20: SUID privilege escalation
├── level_20_to_21.md       # Level 20 -> 21: Background Netcat socket pairing
├── level_21_to_22.md       # Level 21 -> 22: Cron job inspection
├── level_22_to_23.md       # Level 22 -> 23: Reversing dynamic MD5 hashes
├── level_23_to_24.md       # Level 23 -> 24: Cron spool directory script injection
├── level_24_to_25.md       # Level 24 -> 25: Bash brute-force PIN pipeline
├── level_25_to_26.md       # Level 25 -> 26: Restricted shell breakout (more -> vi)
└── level_26_to_27.md       # Level 26 -> 27: Shell escalation via SUID (In Progress)
```

---

## 🛠️ Security Disclaimer

All techniques and writeups documented in this repository were conducted in a strictly authorized educational environment on the [OverTheWire](https://overthewire.org) wargame platform for security research and Linux administration training.
