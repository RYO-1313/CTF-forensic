# 🛡️ MasterKee — Root-Me Writeup

**Platform:** Root-Me &nbsp;|&nbsp; **Category:** Forensics &nbsp;|&nbsp; **Difficulty:** Medium

---

## 🔍 What the challenge was

Two files were provided: a Windows memory dump (`.DMP`) and a KeePass password database (`.kdbx`). The premise was that a colleague claims only he can access his system because he's the only one who knows the master password. The goal was to prove otherwise — by recovering the master password from memory and opening the database without him present.

---

## 🧠 What I learned

- **CVE-2023-32784:** KeePass 2.x has a vulnerability where the master password is recoverable from process memory. Because of how the `SecureTextBoxEx` input control works internally, each character typed leaves a recoverable string artifact in memory — and this persists even after KeePass has been closed.
- The first character of the password is never fully recoverable through this method — the tool always returns a set of candidates rather than a single character. The correct character has to be deduced through reasoning or brute force.
- **KDBX4 format compatibility:** Not all KeePass tools support all database versions. `kpcli` only supports up to KDBX 3.1 and silently fails on KDBX4 — `keepassxc-cli` or the KeePassXC GUI is required for newer databases.
- Flags and sensitive data in KeePass are not always in the password field — the **Notes** field is worth checking too.

---

## 🛠️ My Approach

1. Ran `file` on both files — confirmed a Windows Mini DuMP (17 streams, Feb 2024) and a KeePass KDBX4 database.
2. Recognized the memory dump + KeePass combination as a classic CVE-2023-32784 scenario.
3. Ran the `keepass-dump-masterkey` PoC tool against the dump and received:
   ```
   ●{e, 3, D, H, B, q, a, ...}here_Is_My_V3ry_S3cr3t_P4ssw0rd2024!
   ```
4. The `●` represents the ambiguous first character — looked at the readable structure of the rest and deduced `H`, giving: `Here_Is_My_V3ry_S3cr3t_P4ssw0rd2024!`
5. Attempted to open the database with `kpcli` — it rejected the file because KDBX4 is not supported. Switched to KeePassXC GUI.
6. Entered the recovered password, opened the database, and found the flag in the **Notes** field of an entry named `flag`.

**Note on persistence:** On my first attempt, the tool only returned a reduced candidate set `{e, 3, 9, q}` — none of which worked. Rather than giving up, I came back, reran the tool, and got the full output. In forensic work, tools don't always behave deterministically — a failed first run is not a final answer.

---

## 💡 Key Skill Learned/Reinforced

Understanding how application memory can betray secrets that the user believes are protected. A closed application is not the same as a safe application — if a process has written sensitive data to memory, that data can outlive the session and remain recoverable in a dump.

---

## 🔑 Core Takeaway

Password managers are only as secure as the environment they run in. CVE-2023-32784 is a real, patched vulnerability — but it demonstrates a broader principle: memory is a forensic surface. If an attacker or investigator can access a memory dump from a machine where a password manager was running, the master password may be recoverable regardless of how strong it is. The flag itself reinforces this: `RM{Upd4T3_KeEPas5_t0_2.54}` — update KeePass.

---

## 🤖 Claude's Role

Guided the identification of CVE-2023-32784 as the relevant vulnerability and helped troubleshoot tool compatibility issues (`kpcli` vs `keepassxc-cli`). Also helped reason through the ambiguous first-character candidate set. All tool execution, password recovery, and flag discovery were performed independently.
