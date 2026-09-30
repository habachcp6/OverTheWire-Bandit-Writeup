# Bandit Level 17 → Level 18

| Key | Value |
|:---|:---|
| **Objective** | Compare two files (`passwords.old` and `passwords.new`) in the home directory and extract the single line that changed. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit17` |
| **Password** | `SSH Private Key (file bandit17.key)` |
| **Key Commands** | `diff passwords.old passwords.new` |

---

## Challenge Description

There are 2 files in the homedirectory: `passwords.old` and `passwords.new`. The password for the next level is in `passwords.new` and is the only line that has been changed between `passwords.old` and `passwords.new`.

---

## Technical Analysis

### File Difference Comparison (`diff`)
1. **Differential Analysis**:
   The `diff` utility compares files line-by-line and outputs differences in unified or normal format.
2. **Interpreting `diff` Output**:
   - `< line`: Content present in the first file (`passwords.old`).
   - `> line`: Content present in the second file (`passwords.new`) — this represents the updated password for `bandit18`.

---

## Solution Walkthrough

### Step 1: Connect to Bandit 17 via SSH Key
```bash
ssh -i /tmp/b16_key/bandit17.key bandit17@bandit.labs.overthewire.org -p 2220
```

### Step 2: Compare the Two Files
```bash
diff passwords.old passwords.new
```
**Output:**
```text
42c42
< 0uB7zK492Z4Kz5xT60Z86K856b3Z4521
---
> OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

---

## Password Found

```text
OQxXZjELndr90zuhOTDYBEomI0SZITXI
```

---

## Key Takeaways

- Use `diff <file1> <file2>` to instantly identify modified records between revisions.
- `>` denotes lines added/changed in the second file.

---

[← Previous Level](level_16_to_17.md) | [Summary](README.md) | [Next Level →](level_18_to_19.md)
