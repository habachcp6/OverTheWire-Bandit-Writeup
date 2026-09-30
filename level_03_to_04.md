# Bandit Level 3 → Level 4

| Key | Value |
|:---|:---|
| **Objective** | Locate and read a hidden file situated inside the `inhere` directory. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit3` |
| **Password** | `7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME` |
| **Key Commands** | `ls -la`, `ls -A inhere/`, `cat inhere/...Hiding-From-You` |

---

## 🎯 Challenge Description

The password for the next level is stored in a hidden file in the `inhere` directory.

---

## 🔬 Technical Analysis

### Unix Hidden Files (Dotfiles)
1. **Dotfile Convention**:
   In Unix systems, any file or directory whose name starts with a period (`.`) is considered a hidden file (e.g., `.bashrc`, `.hidden`).
2. **Directory Listing Filters**:
   By default, standard `ls` filters out entries starting with `.`. To view hidden entries:
   - `ls -a` (*all*): Lists all entries including `.` (current directory) and `..` (parent directory).
   - `ls -A` (*almost all*): Lists hidden files while excluding `.` and `..`.

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
# Password: 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

### Step 2: Inspect the `inhere` Directory
```bash
ls -la inhere/
```
**Output:**
```text
total 12
drwxr-xr-x 2 root    root    4096 Jul 20 12:00 .
drwxr-xr-x 3 root    root    4096 Jul 20 12:00 ..
-rw-r----- 1 bandit4 bandit3   33 Jul 20 12:00 ...Hiding-From-You
```

### Step 3: Read the Hidden File
```bash
cat inhere/...Hiding-From-You
```
**Output:**
```text
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

---

## 🔑 Password Found

```text
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

---

## 💡 Key Takeaways

- Files beginning with a `.` are hidden by default from directory listings.
- Use `ls -la` or `ls -A` to discover hidden configuration files and artifacts.

---

[← Previous Level](level_02_to_03.md) | [📋 Summary](README.md) | [Next Level →](level_04_to_05.md)
