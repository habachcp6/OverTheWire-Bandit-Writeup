# Bandit Level 10 → Level 11

| Key | Value |
|:---|:---|
| **Objective** | Decode a Base64-encoded string stored inside `data.txt`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit10` |
| **Password** | `B0s2khmbT9u0geKuOoVGW3JZKhndE3BG` |
| **Key Commands** | `base64 -d data.txt` |

---

## 🎯 Challenge Description

The password for the next level is stored in the file `data.txt`, which contains base64 encoded data.

---

## 🔬 Technical Analysis

### Base64 Encoding Mechanism
1. **Base64 Representation**:
   Base64 is a binary-to-text encoding scheme that represents binary data in an ASCII string format by translating 24 bits of input into four 6-bit Base64 digits (`A-Z`, `a-z`, `0-9`, `+`, `/`, with `=` padding).
2. **Decoding with `base64`**:
   - `base64 <file>`: Encodes data into Base64.
   - `base64 -d <file>`: Decodes Base64 data back into its original plaintext representation.

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
# Password: B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

### Step 2: Decode Base64 Data
```bash
base64 -d data.txt
```
**Output:**
```text
The password is pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

---

## 🔑 Password Found

```text
pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

---

## 💡 Key Takeaways

- Base64 is an encoding format (not encryption) used for safe transmission over text channels.
- Use `base64 -d` to decode Base64 encoded files or STDIN streams.

---

[← Previous Level](level_09_to_10.md) | [📋 Summary](README.md) | [Next Level →](level_11_to_12.md)
