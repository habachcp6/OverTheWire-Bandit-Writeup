# Bandit Level 9 → Level 10

| Key | Value |
|:---|:---|
| **Objective** | Extract human-readable password strings preceded by several `=` characters from a binary data file `data.txt`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit9` |
| **Password** | `EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl` |
| **Key Commands** | `strings data.txt | grep "="` |

---

## 🎯 Challenge Description

The password for the next level is stored in the file `data.txt` in one of the few human-readable strings, preceded by several '=' characters.

---

## 🔬 Technical Analysis

### Binary Forensics with `strings`
1. **Filtering Printable Characters from Binary**:
   The `data.txt` file contains non-printable binary bytes. Standard text tools like `grep` may report `Binary file matches` or produce garbled output.
2. **The `strings` Utility**:
   `strings` parses binary streams and extracts contiguous sequences of printable ASCII characters (default length >= 4). Piping the extracted strings into `grep "=="` filters specifically for the password delimiter pattern.

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
# Password: EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

### Step 2: Extract Strings and Filter
```bash
strings data.txt | grep "=="
```
**Output:**
```text
========== the*
========== passwordk
========== is
========== B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

---

## 🔑 Password Found

```text
B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

---

## 💡 Key Takeaways

- Use `strings` to inspect compiled binaries, memory dumps, and corrupt binary files.
- Combine `strings` with `grep` to quickly discover embedded hardcoded keys and credentials.

---

[← Previous Level](level_08_to_09.md) | [📋 Summary](README.md) | [Next Level →](level_10_to_11.md)
