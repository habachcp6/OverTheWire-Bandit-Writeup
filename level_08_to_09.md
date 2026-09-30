# Bandit Level 8 → Level 9

| Key | Value |
|:---|:---|
| **Objective** | Find the only line of text in `data.txt` that occurs exactly once amongst hundreds of duplicated lines. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit8` |
| **Password** | `VR1ljMayciFxbnUokuQmJFw6QC9VKtub` |
| **Key Commands** | `sort data.txt | uniq -u`, `uniq -c` |

---

## Challenge Description

The password for the next level is stored in the file `data.txt` and is the only line of text that occurs only once.

---

## Technical Analysis

### Data Sorting & Deduplication with Unix Pipelines
1. **The `uniq` Requirement**:
   The `uniq` utility detects and filters adjacent repeated lines. If identical lines are scattered throughout an unsorted file, `uniq` will fail to deduplicate them. Therefore, data **must always be pre-sorted** with `sort`.
2. **Unique Line Filtering (`-u`)**:
   - `sort data.txt`: Organizes all identical lines into contiguous blocks.
   - `uniq -u`: Prints **only unique lines** that have no adjacent duplicates (count == 1).
   - Alternatively, `uniq -c` prefixes each line with its frequency count.

---

## Solution Walkthrough

### Step 1: Connect via SSH
```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
# Password: VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```

### Step 2: Pipeline Sort and Uniq
```bash
sort data.txt | uniq -u
```
**Output:**
```text
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

---

## Password Found

```text
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

---

## Key Takeaways

- `uniq` only compares adjacent lines; always pipe through `sort` first.
- `uniq -u` filters for truly unique items occurring exactly once.

---

[← Previous Level](level_07_to_08.md) | [Summary](README.md) | [Next Level →](level_09_to_10.md)
