# Bandit Level 12 → Level 13

| Key | Value |
|:---|:---|
| **Objective** | Reconstruct a binary file from a Hexdump and decompress 9 recursive layers of nested compression formats (gzip, bzip2, tar). |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit12` |
| **Password** | `GROozWPO8QyN0mGrjUkID0WCYkZiQxrN` |
| **Key Commands** | `xxd -r`, `gzip -d`, `bzip2 -d`, `tar -xf` |

---

## 🎯 Challenge Description

The password for the next level is stored in the file `data.txt`, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under `/tmp` in which you can work.

---

## 🔬 Technical Analysis

### Hexdump Reversal & Multi-Layer Compression Analysis
1. **Hexdump Restoration (`xxd -r`)**:
   `xxd` produces formatted hexadecimal representations of files. `xxd -r` (reverse mode) reconstructs the raw binary bytes from the text dump.
2. **File Header Signatures & Decompression Tools**:
   | Magic Number | Format | Required Extension | Decompression Command |
   |:---|:---|:---|:---|
   | `1f 8b` | `gzip` | `.gz` | `mv file file.gz && gzip -d file.gz` |
   | `42 5a 68` | `bzip2` | `.bz2` | `mv file file.bz2 && bzip2 -d file.bz2` |
   | `75 73 74 61 72` | `POSIX tar archive` | `.tar` | `tar -xf file.tar` |
3. **Enforced Extensions**:
   Utilities like `gzip` and `bzip2` refuse to decompress files unless they carry their respective filename extensions (`.gz`, `.bz2`).

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH & Setup Work Directory
```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
# Password: GROozWPO8QyN0mGrjUkID0WCYkZiQxrN

mkdir /tmp/my_work_12 && cd /tmp/my_work_12
cp ~/data.txt .
```

### Step 2: Reverse Hexdump
```bash
xxd -r data.txt > data.bin
```

### Step 3: Decompress Nested Layers Iteratively
Check format with `file` and decompress step-by-step:
```bash
file data.bin # Output: gzip compressed data
mv data.bin data.gz && gzip -d data.gz

file data # Output: bzip2 compressed data
mv data data.bz2 && bzip2 -d data.bz2

file data # Output: gzip compressed data
mv data data.gz && gzip -d data.gz

file data # Output: POSIX tar archive
mv data data.tar && tar -xf data.tar

file data5.bin # Output: POSIX tar archive
tar -xf data5.bin

file data6.bin # Output: bzip2 compressed data
mv data6.bin data6.bz2 && bzip2 -d data6.bz2

file data6 # Output: POSIX tar archive
mv data6 data6.tar && tar -xf data6.tar

file data8.bin # Output: gzip compressed data
mv data8.bin data8.gz && gzip -d data8.gz

file data8 # Output: ASCII text
cat data8
```
**Output:**
```text
The password is qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```

---

## 🔑 Password Found

```text
qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```

---

## 💡 Key Takeaways

- Use `xxd -r` to reconstruct binaries from hexdump text files.
- Always inspect actual magic bytes with `file` instead of relying on file names.
- Rename files to appropriate extensions (`.gz`, `.bz2`, `.tar`) to satisfy archive unpackers.

---

[← Previous Level](level_11_to_12.md) | [📋 Summary](README.md) | [Next Level →](level_13_to_14.md)
