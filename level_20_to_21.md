# Bandit Level 20 → Level 21

| Key | Value |
|:---|:---|
| **Objective** | Start a background TCP listener to send the `bandit20` password to an SUID client program (`suconnect`), which verifies the credential and returns the password for `bandit21`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit20` |
| **Password** | `4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA` |
| **Key Commands** | `nc -lvnp <port> &`, `./suconnect <port>` |

---

## Challenge Description

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

---

## Technical Analysis

### Inter-Process Networking & Job Control
1. **The `suconnect` Architecture**:
   `suconnect` is an SUID binary owned by `bandit21`. It initiates a TCP client connection to `localhost:<port>`, receives a password string, and if valid, writes `/etc/bandit_pass/bandit21` back into the TCP connection.
2. **Background Process Execution (`&`)**:
   Since a single terminal session is used, the Netcat listener must run in the background using `&`:
   `echo "<password>" | nc -lvnp 45454 &`
   When `suconnect 45454` connects, Netcat pipes the password into `suconnect`, which prints the next password back to the terminal.

---

## Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit20@bandit.labs.overthewire.org -p 2220
# Password: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
```

### Step 2: Spawn Background Netcat Listener
Choose any unprivileged port (e.g., `45454`):
```bash
echo "4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA" | nc -lvnp 45454 &
```

### Step 3: Trigger the SUID Client
```bash
./suconnect 45454
```
**Output:**
```text
Connection to localhost 45454 port [tcp/*] succeeded!
Read: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA
Password matches, sending next password
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```

---

## Password Found

```text
bW9kBv5WC3P4yoDyf12LSdGuNz5ka6hY
```

---

## Key Takeaways

- Use `&` to run listening network daemons in the background within a single shell session.
- SUID clients that exchange secrets over local loopback sockets can be spoofed or intercepted.

---

[← Previous Level](level_19_to_20.md) | [Summary](README.md) | [Next Level →](level_21_to_22.md)
