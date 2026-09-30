# Bandit Level 19 → Level 20

| Key | Value |
|:---|:---|
| **Objective** | Use an SUID binary (`bandit20-do`) in the home directory to read `/etc/bandit_pass/bandit20` under elevated privileges. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit19` |
| **Password** | `KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI` |
| **Key Commands** | `./bandit20-do id`, `./bandit20-do cat /etc/bandit_pass/bandit20` |

---

## Challenge Description

To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

---

## Technical Analysis

### Linux SUID (Set User ID) Privilege Model
1. **The SUID Permission Bit**:
   SUID (octal `4000`, represented by `s` in owner execution permissions: `-rwsr-x---`) causes a binary to execute with the Effective User ID (`EUID`) of the **file owner** rather than the calling user (`RUID`).
2. **Privilege Escalation Mechanism**:
   - `bandit20-do` is owned by user `bandit20` with group `bandit19` and has SUID enabled.
   - When executed by `bandit19`, any command passed to `./bandit20-do <command>` runs with EUID = `bandit20`, allowing it to read restricted files like `/etc/bandit_pass/bandit20`.

---

## Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit19@bandit.labs.overthewire.org -p 2220
# Password: KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI
```

### Step 2: Inspect SUID Permissions
```bash
ls -la
```
**Output:**
```text
-rwsr-x--- 1 bandit20 bandit19 14876 Jul 20 12:00 bandit20-do
```

### Step 3: Verify Elevated Execution
```bash
./bandit20-do id
```
**Output:**
```text
uid=11019(bandit19) gid=11019(bandit19) euid=11020(bandit20) groups=11019(bandit19)
```

### Step 4: Read the Password File
```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```
**Output:**
```text
4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```

---

## Password Found

```text
4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```

---

## Key Takeaways

- SUID binaries execute with the permissions of the file owner (EUID).
- Improperly designed SUID binaries that execute arbitrary subcommands lead directly to privilege escalation.

---

[← Previous Level](level_18_to_19.md) | [Summary](README.md) | [Next Level →](level_20_to_21.md)
