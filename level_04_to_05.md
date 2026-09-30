# Bandit Level 4 → Level 5

| Key | Value |
|:---|:---|
| **Objective** | Identify and read the only human-readable (ASCII text) file amongst multiple binary/data files inside the `inhere` directory. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit4` |
| **Password** | `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq` |
| **Key Commands** | `file inhere/*`, `file ./*`, `cat inhere/-file07` |

---

## 🎯 Challenge Description

The password for the next level is stored in the only human-readable file in the `inhere` directory. Tip: if your terminal is messed up, try the `reset` command.

---

## 🔬 Technical Analysis

### File Signature Inspection & MIME Detection
1. **Magic Bytes & Header Inspection**:
   In Linux, file extensions (e.g., `.txt`, `.bin`) are purely decorative. The `file` utility determines the true format of a file by examining its header bytes (*magic numbers*) and character encoding against `/etc/magic` databases.
2. **Identifying ASCII Text**:
   Running `file inhere/*` scans all files in the directory and reports their encoding:
   - `data`: Raw non-printable binary bytes (which corrupts terminal display if `cat` is used).
   - `ASCII text`: Plain printable characters containing the password.

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
# Password: xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

### Step 2: Inspect File Types
```bash
file inhere/*
```
**Output:**
```text
inhere/-file00: data
inhere/-file01: data
inhere/-file02: data
inhere/-file03: data
inhere/-file04: data
inhere/-file05: data
inhere/-file06: data
inhere/-file07: ASCII text
inhere/-file08: data
inhere/-file09: data
```

### Step 3: Read the Human-Readable File
Notice the filename begins with a dash (`-file07`), so relative path syntax is required:
```bash
cat inhere/-file07
```
**Output:**
```text
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

---

## 🔑 Password Found

```text
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

---

## 💡 Key Takeaways

- Use the `file` command to detect file types independently of extensions.
- Avoid `cat` on binary data files as control characters can break terminal formatting.

---

[← Previous Level](level_03_to_04.md) | [📋 Summary](README.md) | [Next Level →](level_05_to_06.md)
