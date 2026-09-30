# Bandit Level 11 → Level 12

| Key | Value |
|:---|:---|
| **Objective** | Decrypt a password obfuscated with the ROT13 substitution cipher in `data.txt`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit11` |
| **Password** | `pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro` |
| **Key Commands** | `tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt` |

---

## Challenge Description

The password for the next level is stored in the file `data.txt`, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions.

---

## Technical Analysis

### Classical Cryptography: ROT13 Substitution Cipher
1. **ROT13 Algorithm**:
   ROT13 (Rotate by 13 places) is a special case of the Caesar substitution cipher. Because the Latin alphabet has 26 letters, shifting by 13 is symmetric: applying ROT13 twice restores the original text ($13 + 13 = 26 \equiv 0 \pmod{26}$).
2. **Character Translation with `tr`**:
   The `tr` utility translates or deletes characters from Standard Input:
   - Target alphabet: `A-Za-z`
   - Replacement map: `N-ZA-Mn-za-m` (shifting letters A-M to N-Z and N-Z to A-M).

---

## Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
# Password: pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

### Step 2: Decode with `tr`
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
**Output:**
```text
The password is GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

---

## Password Found

```text
GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

---

## Key Takeaways

- ROT13 is a simple monoalphabetic substitution cipher with zero cryptographic security.
- Use `tr '<source_chars>' '<target_chars>'` for stream character translation.

---

[← Previous Level](level_10_to_11.md) | [Summary](README.md) | [Next Level →](level_12_to_13.md)
