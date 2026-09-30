# Bandit Level 16 → Level 17

| Key | Value |
|:---|:---|
| **Objective** | Scan ports in the range `31000-32000` to find which one speaks SSL/TLS and credentials-checking logic, submit the `bandit16` password, and capture the returned SSH Private Key for `bandit17`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit16` |
| **Password** | `kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V` |
| **Key Commands** | `nmap -p 31000-32000 localhost`, `openssl s_client` |

---

## Challenge Description

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don't.

---

## Technical Analysis

### Port Scanning & Server Logic Discrimination
1. **Network Reconnaissance with `nmap`**:
   Scanning `nmap -p 31000-32000 localhost` identifies open listening ports. Adding service detection flags (`-sV`) identifies whether a port speaks SSL and how it responds.
2. **Echo Servers vs. Credential Checkers**:
   Some listening ports are simple echo daemons that reflect back whatever you send. The genuine challenge daemon responds with `Correct!` followed by an RSA private key.
3. **SSH Private Key Management**:
   The returned output is an OpenSSH RSA Private Key. To use it for `bandit17`:
   - Save the key to a file in `/tmp/`.
   - Set strict permissions: `chmod 600 keyfile`.

---

## Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit16@bandit.labs.overthewire.org -p 2220
# Password: kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```

### Step 2: Scan Port Range
```bash
nmap -p 31000-32000 -sV localhost
```
**Identified Ports:**
- `31518`: Echo daemon
- `31790`: SSL/TLS Credential service

### Step 3: Connect to Port 31790 with OpenSSL
```bash
openssl s_client -quiet -connect localhost:31790
```
Submit password:
```text
kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V
```
**Output:**
```text
Correct!
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
... [Truncated Key Content] ...
piuGIiYum5tM5RAAAADnJ1ZHlAbG9jYWxob3N0AQIDBA==
-----END OPENSSH PRIVATE KEY-----
```

### Step 4: Save and Secure the Key
```bash
mkdir /tmp/b16_key && cd /tmp/b16_key
cat << 'EOF' > bandit17.key
-----BEGIN OPENSSH PRIVATE KEY-----
[PASTE KEY HERE]
-----END OPENSSH PRIVATE KEY-----
EOF

chmod 600 bandit17.key
```

---

## Password Found

```text
SSH Private Key (file bandit17.key)
```

---

## Key Takeaways

- Use `nmap` port scanning to identify active services across port ranges.
- Private keys must be protected with `chmod 600` permissions to be usable by OpenSSH.

---

[← Previous Level](level_15_to_16.md) | [Summary](README.md) | [Next Level →](level_17_to_18.md)
