# Bandit Level 2 → Level 3

| Key | Value |
|:---|:---|
| **Objective** | Read the password from a file containing whitespace characters in its name: `spaces in this filename`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit2` |
| **Password** | `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB` |
| **Key Commands** | `cat "spaces in this filename"`, `cat spaces\ in\ this\ filename` |

---

## Challenge Description

The password for the next level is stored in a file called `spaces in this filename` located in the home directory.

---

## Technical Analysis

### Shell Word Splitting & Whitespace Handling
1. **Whitespace as Argument Delimiters**:
   The Bash shell uses whitespace characters (spaces, tabs, newlines) defined in the `$IFS` (Internal Field Separator) variable to split commands into distinct arguments. Running `cat spaces in this filename` causes `cat` to search for four separate files: `spaces`, `in`, `this`, and `filename`, resulting in `No such file or directory` errors.
2. **Quoting and Escaping Techniques**:
   - **Double / Single Quotes (`"..."` / `'...'`)**: Preserves the literal string value including all whitespace as a single argument.
   - **Backslash Escape (`\ `)**: Removes the special syntactic meaning of the subsequent character, treating space as a literal character.

---

## Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
# Password: PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

### Step 2: Read the File with Spaces

**Method 1 (Double Quotes):**
```bash
cat "spaces in this filename"
```

**Method 2 (Backslash Escaping):**
```bash
cat spaces\ in\ this\ filename
```

**Method 3 (Tab Autocompletion):**
Type `cat spa` and press `Tab` on your keyboard. Bash will automatically escape the spaces.

**Output:**
```text
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

---

## Password Found

```text
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

---

## Key Takeaways

- Spaces in filenames cause shells to split them into separate command arguments.
- Enclosing names in quotes or escaping spaces with `\` handles whitespace safely.
- Use Tab autocompletion to allow the shell to automatically format complex filenames.

---

[← Previous Level](level_01_to_02.md) | [Summary](README.md) | [Next Level →](level_03_to_04.md)
