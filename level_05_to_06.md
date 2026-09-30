# Bandit Level 5 → Level 6

| Key | Value |
|:---|:---|
| **Objective** | Find a file in the `inhere` directory matching three specific criteria: human-readable, exactly 1033 bytes in size, and non-executable. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit5` |
| **Password** | `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG` |
| **Key Commands** | `find inhere/ -type f -size 1033c ! -executable` |

---

## 🎯 Challenge Description

The password for the next level is stored in a file somewhere under the `inhere` directory and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

---

## 🔬 Technical Analysis

### Deep File Searching with `find`
1. **Filtering by Size (`-size`)**:
   - `1033c`: Exactly 1033 bytes (`c` stands for bytes/characters).
   - `1033k`: Kilobytes, `1033M`: Megabytes.
2. **Filtering by File Type (`-type`)**:
   - `-type f`: Regular files only (excludes directories, sockets, symbolic links).
3. **Filtering by Permissions & Inversion (`!`)**:
   - `-executable`: Matches executable files.
   - `! -executable`: Inverts the match to find non-executable files.

---

## 🚀 Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
# Password: 6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

### Step 2: Search for the Matching File
```bash
find inhere/ -type f -size 1033c ! -executable
```
**Output:**
```text
inhere/maybehere07/.file2
```

### Step 3: Read the Target File
```bash
cat inhere/maybehere07/.file2
```
**Output:**
```text
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```

---

## 🔑 Password Found

```text
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```

---

## 💡 Key Takeaways

- The `find` utility is essential for locating files across nested directory trees.
- `-size <N>c` matches exact byte sizes, while `!` negates matching expressions.

---

[← Previous Level](level_04_to_05.md) | [📋 Summary](README.md) | [Next Level →](level_06_to_07.md)
