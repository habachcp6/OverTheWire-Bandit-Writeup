# Bandit Level 7 → Level 8

| Key | Value |
|:---|:---|
| **Objective** | Extract the password located next to the keyword `millionth` in a large data file `data.txt`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit7` |
| **Password** | `Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3` |
| **Key Commands** | `grep "millionth" data.txt`, `awk` |

---

## Challenge Description

The password for the next level is stored in the file `data.txt` next to the word `millionth`.

---

## Technical Analysis

### Fast Text Pattern Matching with `grep`
1. **Grep Utility**:
   `grep` (Global Regular Expression Print) scans files line-by-line using optimized string matching algorithms (Boyer-Moore pattern matching) to output only lines matching a given pattern.
2. **Processing Large Text Streams**:
   In large datasets (thousands of lines), manual inspection is impractical. `grep "millionth" data.txt` searches `data.txt` directly without needing intermediate pipes (`cat file | grep`).

---

## Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
# Password: Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```

### Step 2: Search for the Keyword
```bash
grep "millionth" data.txt
```
**Output:**
```text
millionth	VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```

---

## Password Found

```text
VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```

---

## Key Takeaways

- `grep <pattern> <file>` quickly extracts matching records from massive text files.
- Directly passing the filename to `grep` is more efficient than piping from `cat`.

---

[← Previous Level](level_06_to_07.md) | [Summary](README.md) | [Next Level →](level_08_to_09.md)
