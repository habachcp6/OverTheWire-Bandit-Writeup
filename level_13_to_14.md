# Bandit Level 13 → Level 14

| Key | Value |
|:---|:---|
| **Objective** | Authenticate to `bandit14` on `localhost` using an OpenSSH Private Key (`sshkey.private`) and retrieve the password from `/etc/bandit_pass/bandit14`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit13` |
| **Password** | `qQYQiHOBPR8zR61qxYqX45quvihF2uzk` |
| **Key Commands** | `ssh -i sshkey.private bandit14@localhost -p 2220` |

---

## 🎯 Challenge Description

The password for the next level is stored in `/etc/bandit_pass/bandit14` and can only be read by user bandit14. For this level, you don't get the next password, but you get a private SSH key that can be used to log into the next level.

---

## 🔬 Technical Analysis

### Asymmetric Cryptography & SSH Key-Based Authentication
1. **Public Key vs. Private Key**:
   In asymmetric SSH authentication:
   - The Public Key is placed in the destination account's `~/.ssh/authorized_keys`.
   - The Private Key (`sshkey.private`) is retained by the user to sign cryptographic authentication challenges.
2. **Connecting to Localhost**:
   Because `bandit13` and `bandit14` exist on the same server, `localhost` (or `127.0.0.1`) on port `2220` can be used directly as the connection destination.
3. **Private Key File Permissions**:
   OpenSSH mandates strict file permissions on private keys (`chmod 600` or `400`). If a key is readable by other users (`0777` or `0644`), the client will reject it.

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
# Password: qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```

### Step 2: Use the Private Key to Log into Bandit 14
```bash
ssh -i sshkey.private bandit14@localhost -p 2220 -o StrictHostKeyChecking=no
```

### Step 3: Retrieve the Password
Once authenticated as `bandit14@bandit:~$`:
```bash
cat /etc/bandit_pass/bandit14
```
**Output:**
```text
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

---

## 🔑 Password Found

```text
aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

---

## 💡 Key Takeaways

- SSH key pairs allow passwordless cryptographic authentication.
- Target-level passwords on OverTheWire reside in `/etc/bandit_pass/bandit<N>`.

---

[← Previous Level](level_12_to_13.md) | [📋 Summary](README.md) | [Next Level →](level_14_to_15.md)
