# Bandit Level 15 → Level 16

| Key | Value |
|:---|:---|
| **Objective** | Submit the password of `bandit15` to an SSL/TLS encrypted daemon listening on `localhost:30001`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit15` |
| **Password** | `pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7` |
| **Key Commands** | `openssl s_client -connect localhost:30001 -ign_eof` |

---

## 🎯 Challenge Description

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

---

## 🔬 Technical Analysis

### Encrypted Transport Layer (SSL/TLS) Communication
1. **Netcat Limitation on Encrypted Sockets**:
   Plain Netcat communicates in cleartext. Connecting `nc` to an SSL/TLS port triggers a protocol error or binary TLS handshake garbage (`Client Hello` failure).
2. **OpenSSL `s_client`**:
   `openssl s_client` is a diagnostic tool that initiates an SSL/TLS handshake with a remote server, verifies certificates, and opens an interactive encrypted session.
   - `-connect <host>:<port>`: Target socket address.
   - `-ign_eof`: Prevents session termination when input stream ends.
   - `-quiet`: Suppresses verbose certificate and session parameters.

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit15@bandit.labs.overthewire.org -p 2220
# Password: pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

### Step 2: Establish SSL/TLS Connection
```bash
openssl s_client -quiet -connect localhost:30001
```
Paste the password for `bandit15`:
```text
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```
**Output:**
```text
Correct!
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
closed
```

---

## 🔑 Password Found

```text
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

---

## 💡 Key Takeaways

- Encrypted ports require dedicated TLS clients like `openssl s_client` or `socat`.
- Use `openssl s_client -quiet` to suppress verbose certificate metadata.

---

[← Previous Level](level_14_to_15.md) | [📋 Summary](README.md) | [Next Level →](level_16_to_17.md)
