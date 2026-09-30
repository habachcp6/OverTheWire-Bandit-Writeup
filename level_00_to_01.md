# Bandit Level 0 → Level 1

| Key | Value |
|:---|:---|
| **Objective** | Connect to the wargame server via SSH using the default credentials and retrieve the password for bandit1 stored in a file named `readme`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit0` |
| **Password** | `bandit0` |
| **Key Commands** | `ssh`, `ls`, `cat`, `pwd` |

---

## 🎯 Challenge Description

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is `bandit.labs.overthewire.org`, on port `2220`. The username is `bandit0` and the password is `bandit0`. Once logged in, read the file `readme` located in the home directory.

---

## 🔬 Technical Analysis

### Linux File System & SSH Basics
1. **Secure Shell (SSH) Protocol**:
   SSH is an encrypted network protocol used for remote command execution and secure data communication. In standard Unix systems, SSH defaults to port `22`. However, OverTheWire maps its public-facing challenges to port `2220`. The `-p` flag specifies the destination TCP port.
2. **File Inspection (`cat` command)**:
   The `cat` utility (short for *concatenate*) reads data from files sequentially and prints them to Standard Output (`STDOUT`, file descriptor `1`). Since `readme` is located directly in the login directory (`~` or `/home/bandit0`), it can be referenced using its relative path.

---

## 🚀 Solution Walkthrough

### Step 1: Establish SSH Connection
Open your terminal and connect to the OverTheWire server:
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
When prompted for the password, enter:
```text
bandit0
```

### Step 2: List Directory Contents
Verify the presence of files in your current working directory:
```bash
ls -la
```
**Output:**
```text
total 24
drwxr-xr-x  2 root    root    4096 Jul 20 12:00 .
drwxr-xr-x 70 root    root    4096 Jul 20 12:00 ..
-rw-r--r--  1 root    root     220 Jul 20 12:00 .bash_logout
-rw-r--r--  1 root    root    3771 Jul 20 12:00 .bashrc
-rw-r--r--  1 root    root     807 Jul 20 12:00 .profile
-rw-r-----  1 bandit1 bandit0   33 Jul 20 12:00 readme
```

### Step 3: Read the Password File
Read the content of `readme`:
```bash
cat readme
```
**Output:**
```text
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

---

## 🔑 Password Found

```text
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

---

## 💡 Key Takeaways

- SSH connections on non-standard ports require the `-p <port>` parameter.
- `ls -la` lists all files including hidden dotfiles with permissions and ownership.
- `cat <file>` outputs raw file content to the terminal.

---

[← Level 0] | [📋 Summary](README.md) | [Next Level →](level_01_to_02.md)
