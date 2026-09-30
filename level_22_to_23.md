# Bandit Level 22 → Level 23

| Key | Value |
|:---|:---|
| **Objective** | Reverse-engineer a shell script executed by cron that generates dynamic target filenames using an MD5 hash calculation for user `bandit23`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit22` |
| **Password** | `RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz` |
| **Key Commands** | `cat /usr/bin/cronjob_bandit23.sh`, `echo I am user bandit23 | md5sum` |

---

## 🎯 Challenge Description

A program is running automatically at regular intervals from `cron`, the time-based job scheduler. Look in `/etc/cron.d/` for the configuration and see what command is being executed.

---

## 🔬 Technical Analysis

### Reverse Engineering Shell Logic & Dynamic Hashing
1. **Inspecting `/usr/bin/cronjob_bandit23.sh`**:
   ```bash
   myname=$(whoami)
   mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
   cat /etc/bandit_pass/$myname > /tmp/$mytarget
   ```
2. **Replicating Hash Generation for `bandit23`**:
   When the cron daemon executes the script as `bandit23`, `whoami` returns `bandit23`. The target file is:
   `echo "I am user bandit23" | md5sum | cut -d ' ' -f 1`
   Calculating this hash reveals the exact filename in `/tmp/`.

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit22@bandit.labs.overthewire.org -p 2220
# Password: RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz
```

### Step 2: Read the Cron Job Script
```bash
cat /usr/bin/cronjob_bandit23.sh
```

### Step 3: Compute Target MD5 Hash for `bandit23`
```bash
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
```
**Output:**
```text
8ca319486bfbbc3663ea0fbe81326349
```

### Step 4: Read the Generated File
```bash
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```
**Output:**
```text
gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw
```

---

## 🔑 Password Found

```text
gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw
```

---

## 💡 Key Takeaways

- Deconstruct script variables and emulate execution environments to find dynamically named assets.
- Deterministic hash algorithms (MD5) without secret salts are completely predictable.

---

[← Previous Level](level_21_to_22.md) | [📋 Summary](README.md) | [Next Level →](level_23_to_24.md)
