# Bandit Level 1 → Level 2

| Key | Value |
|:---|:---|
| **Objective** | Read the password stored in a file named `-` (a single dash/hyphen) located in the home directory. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit1` |
| **Password** | `6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR` |
| **Key Commands** | `cat ./-`, `cat < -`, `cat -- -` |

---

## Challenge Description

The password for the next level is stored in a file called `-` located in the home directory.

---

## Technical Analysis

### Command-Line Argument Parsing Pitfalls
In Unix-like systems and POSIX command-line utilities:
1. **The Hyphen (`-`) as Command Options**:
   CLI utilities interpret arguments beginning with `-` as configuration flags or options (e.g., `-h`, `-v`). When executing `cat -`, the utility treats `-` as a special token representing Standard Input (`STDIN`) rather than a filename on disk. As a result, the terminal halts waiting for interactive keyboard input.
2. **Path Disambiguation (`./-` or `--`)**:
   - **Relative Path Prefix (`./`)**: Specifying `./-` explicitly tells the shell and system calls (`open()`) that `-` is an inode entry residing in the current directory (`.`), not an option flag.
   - **End-of-Command Options (`--`)**: In POSIX standard utilities, a double dash `--` signals the end of command options. All subsequent arguments are parsed strictly as positional filenames.

---

## Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
# Password: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

### Step 2: Read the Dashed File
Attempting `cat -` will hang waiting for STDIN. Use any of the following bypass techniques:

**Method 1 (Relative Path Prefix - Recommended):**
```bash
cat ./-
```

**Method 2 (End-of-Options delimiter):**
```bash
cat -- -
```

**Method 3 (Shell Input Redirection):**
```bash
cat < -
```

**Output:**
```text
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

---

## Password Found

```text
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

---

## Key Takeaways

- A single `-` represents STDIN in most Linux CLI tools.
- Always prefix special/unsafe filenames with `./` to prevent argument injection.
- The `--` delimiter forces utilities to treat all following arguments as plain filenames.

---

[← Previous Level](level_00_to_01.md) | [Summary](README.md) | [Next Level →](level_02_to_03.md)
