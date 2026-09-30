# Bandit Level 26 → Level 27

| Key | Value |
|:---|:---|
| **Objective** | Escape into an interactive Bash shell from within `vi` and execute the SUID binary `bandit27-do` to capture the password for `bandit27`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit26` |
| **Password** | `jHdv2ELQhT22BkprMNDjybZDAkw1zeBJ` |
| **Key Commands** | `:set shell=/bin/bash`, `:shell`, `./bandit27-do cat /etc/bandit_pass/bandit27` |

---

## Challenge Description

Good job getting a shell! Now hurry and grab the password for bandit27!

---

## Technical Analysis

### Shell Hijacking from Editor & SUID Execution
1. **Spawning Interactive Shell from `vi`**:
   Inside `vi`, the default execution shell can be reconfigured:
   `:set shell=/bin/bash`
   Executing `:shell` suspends `vi` and invokes an interactive Bash session under `bandit26`.
2. **Executing the SUID Binary**:
   In `/home/bandit26`, the file `bandit27-do` is an SUID binary owned by `bandit27`. Running `./bandit27-do cat /etc/bandit_pass/bandit27` outputs the target password.

---

## Solution Walkthrough

### Step 1: Break Out of `vi` into Bash
While inside `vi` from Level 25→26:
```text
:set shell=/bin/bash
:shell
```

### Step 2: Verify Interactive Shell & List Directory
```bash
id
ls -la
```
**Output:**
```text
uid=11026(bandit26) gid=11026(bandit26) groups=11026(bandit26)
-rwsr-x--- 1 bandit27 bandit26 14876 Jul 20 12:00 bandit27-do
```

### Step 3: Execute SUID Binary to Retrieve Bandit 27 Password
```bash
./bandit27-do cat /etc/bandit_pass/bandit27
```

*(Challenge in progress)*

---

## Password Found

```text
*(In Progress / Pending)*
```

---

## Key Takeaways

- Text editors with shell invocation capabilities (`:shell`, `:!`) permit full shell breakout from restricted environments.
- SUID binaries (`bandit27-do`) allow command execution with the privileges of the file owner.

---

[← Previous Level](level_25_to_26.md) | [Summary](README.md) | [Next Level → (Pending)]
