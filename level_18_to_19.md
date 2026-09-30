# Bandit Level 18 → Level 19

| Key | Value |
|:---|:---|
| **Objective** | Read the password stored in `readme` despite the user's `.bashrc` automatically closing the connection with `Byebye !` upon login. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit18` |
| **Password** | `OQxXZjELndr90zuhOTDYBEomI0SZITXI` |
| **Key Commands** | `ssh bandit18@host -p 2220 "cat readme"` |

---

## Challenge Description

The password for the next level is stored in a file `readme` in the homedirectory. Unfortunately, someone has modified `.bashrc` to log you out when you log in with SSH.

---

## Technical Analysis

### SSH Shell Initialization vs. Non-Interactive Command Execution
1. **Interactive Shell vs. `.bashrc`**:
   When establishing an interactive SSH session, the server invokes an interactive login shell, sourcing startup scripts (`/etc/profile`, `~/.bash_profile`, `~/.bashrc`). Because `bandit18`'s `.bashrc` contains `echo 'Byebye !'; exit`, interactive logins terminate immediately.
2. **Non-Interactive Command Execution Bypass**:
   Passing a command directly at the end of the `ssh` invocation (e.g., `ssh user@host "cat readme"`) executes the target binary in **non-interactive mode**, completely bypassing `.bashrc` execution.

---

## Solution Walkthrough

### Step 1: Execute Direct Remote Command via SSH
```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```
When prompted, enter the password:
```text
OQxXZjELndr90zuhOTDYBEomI0SZITXI
```
**Output:**
```text
KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI
```

---

## Password Found

```text
KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI
```

---

## Key Takeaways

- Non-interactive SSH commands (`ssh user@host "cmd"`) do not load interactive startup scripts like `.bashrc`.
- This technique allows operators to bypass rogue or broken login environments.

---

[← Previous Level](level_17_to_18.md) | [Summary](README.md) | [Next Level →](level_19_to_20.md)
