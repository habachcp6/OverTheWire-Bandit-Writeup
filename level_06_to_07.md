# Bandit Level 6 → Level 7

| Key | Value |
|:---|:---|
| **Objective** | Locate a file somewhere on the entire server belonging to user `bandit7`, owned by group `bandit6`, and exactly 33 bytes in size. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit6` |
| **Password** | `pXa26xhMWaC2SvDotA4r9EgZkulOeSBW` |
| **Key Commands** | `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null` |

---

## Challenge Description

The password for the next level is stored somewhere on the server and has all of the following properties:
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

---

## Technical Analysis

### System-Wide Searches & STDERR Redirection
1. **Ownership Filtering**:
   - `-user bandit7`: Matches files owned by UID corresponding to `bandit7`.
   - `-group bandit6`: Matches files belonging to GID corresponding to `bandit6`.
   - `-size 33c`: Exactly 33 bytes.
2. **I/O Redirection & Error Suppression (`2>/dev/null`)**:
   Searching from root (`/`) scans system directories (e.g., `/proc`, `/root`, `/sys`) where normal users lack read permissions. This triggers hundreds of `Permission denied` errors on Standard Error (`STDERR`, file descriptor `2`).
   - `2>/dev/null` discards all error messages into the null device, leaving only clean Standard Output (`STDOUT`, file descriptor `1`).

---

## Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
# Password: pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```

### Step 2: Execute System-Wide Search with Error Redirection
```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
**Output:**
```text
/var/lib/dpkg/info/bandit7.password
```

### Step 3: Read the Target File
```bash
cat /var/lib/dpkg/info/bandit7.password
```
**Output:**
```text
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```

---

## Password Found

```text
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```

---

## Key Takeaways

- Linux file ownership is tracked via User (UID) and Group (GID).
- Redirecting errors with `2>/dev/null` eliminates noise during privilege-restricted scans.

---

[← Previous Level](level_05_to_06.md) | [Summary](README.md) | [Next Level →](level_07_to_08.md)
