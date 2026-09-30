# Bandit Level 21 → Level 22

| Key | Value |
|:---|:---|
| **Objective** | Inspect system cron daemon configurations in `/etc/cron.d/` to locate a scheduled job copying `bandit22`'s password to a readable target file in `/tmp`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit21` |
| **Password** | `bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY` |
| **Key Commands** | `cat /etc/cron.d/cronjob_bandit22`, `cat /usr/bin/cronjob_bandit22.sh` |

---

## Challenge Description

A program is running automatically at regular intervals from `cron`, the time-based job scheduler. Look in `/etc/cron.d/` for the configuration and see what command is being executed.

---

## Technical Analysis

### Linux Scheduled Tasks (Cron Jobs)
1. **Cron Configuration Architecture**:
   The `cron` daemon executes scheduled commands defined in `/etc/crontab` and `/etc/cron.d/`.
   Format: `* * * * * <user> <command_to_run>`
2. **Reviewing Scheduled Shell Scripts**:
   Reading `/etc/cron.d/cronjob_bandit22` reveals a job running as user `bandit22`:
   `@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null`
   `* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null`
   Inspecting `/usr/bin/cronjob_bandit22.sh` reveals the target output path where the password is copied.

---

## Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit21@bandit.labs.overthewire.org -p 2220
# Password: bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```

### Step 2: Check Cron Configurations
```bash
cat /etc/cron.d/cronjob_bandit22
```
**Output:**
```text
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

### Step 3: Read the Executed Shell Script
```bash
cat /usr/bin/cronjob_bandit22.sh
```
**Output:**
```bash
#!/bin/sh
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

### Step 4: Read the Generated Password File
```bash
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
**Output:**
```text
RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz
```

---

## Password Found

```text
RYVux2rHEm9tiXHmLFzuR7Vhx6AZQMEz
```

---

## Key Takeaways

- Always inspect `/etc/cron*` during Linux privilege escalation reconnaissance.
- World-readable files created by privileged cron jobs expose sensitive credentials.

---

[← Previous Level](level_20_to_21.md) | [Summary](README.md) | [Next Level →](level_22_to_23.md)
