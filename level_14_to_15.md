# Bandit Level 14 → Level 15

| Key | Value |
|:---|:---|
| **Objective** | Submit the password of `bandit14` to a network daemon listening on `localhost:30000` to receive the password for `bandit15`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit14` |
| **Password** | `aaWecNkG4FhxJQxz07uiwzVP6bJiYS65` |
| **Key Commands** | `nc localhost 30000`, `telnet` |

---

## 🎯 Challenge Description

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

---

## 🔬 Technical Analysis

### Raw TCP Socket Communication with Netcat
1. **Netcat (`nc`) as TCP Client**:
   Netcat is the 'Swiss Army knife' of networking. Running `nc <host> <port>` establishes a raw TCP stream connection, binding the terminal's `STDIN` to the remote socket's input and remote socket's output to local `STDOUT`.
2. **Automating Input via Pipelines**:
   Input can be transmitted interactively or piped directly:
   `echo "<password>" | nc localhost 30000` or `nc localhost 30000 < /etc/bandit_pass/bandit14`.

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit14@bandit.labs.overthewire.org -p 2220
# Password: aaWecNkG4FhxJQxz07uiwzVP6bJiYS65
```

### Step 2: Send Password via Netcat Pipeline
```bash
echo "aaWecNkG4FhxJQxz07uiwzVP6bJiYS65" | nc localhost 30000
```
**Output:**
```text
Correct!
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

---

## 🔑 Password Found

```text
pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7
```

---

## 💡 Key Takeaways

- Use `nc <host> <port>` to interact with plain-text TCP socket services.
- Pipes allow seamless automation of network payload delivery.

---

[← Previous Level](level_13_to_14.md) | [📋 Summary](README.md) | [Next Level →](level_15_to_16.md)
