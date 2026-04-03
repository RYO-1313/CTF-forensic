# 🔬 CTF Forensics — Root-Me
Documenting a self-taught journey through forensics challenges on Root-Me, with a focus on building SOC Analyst fundamentals and analytical methodology.

---

## 👤 About Me

Self-taught cybersecurity student targeting a career as a SOC Analyst, with a long-term goal of transitioning into Red Team operations. I practice daily on Root-Me and TryHackMe (Blue Team pathways), and document every challenge to reinforce learning and build a professional portfolio.

- 🐧 Daily Linux user (CachyOS + Kali Linux VM)
- 🔵 TryHackMe — Blue Team pathways
- 🌐 Parallel repo: [CTF Networking — Root-Me](https://github.com/RYO-1313/CTF-Networking-Root-Me)

---

## 🧰 Tools Used

| Tool | Purpose |
|------|---------|
| `file` | File type identification and initial recon |
| `strings` | Human-readable text extraction from binary files |
| `grep` | Pattern-based filtering of command-line output |
| `foremost` | File carving and recovery from raw disk images |
| `binwalk` | Embedded file signature detection in binary images |
| `exiftool` | Metadata extraction and analysis from media files |
| `guestmount` | Safe read-only mounting of virtual disk images |

---

## 📚 Challenges Completed

| # | Challenge | Category | Difficulty | Status |
|---|-----------|----------|------------|--------|
| 01 | [Deleted File](./01-Deleted-File.md) | Forensics | Very Easy | ✅ |
| 02 | [Command & Control - Level 2](./02-Command-And-Control-Level-2.md) | Forensics | Easy | ✅ |
| 03 | [Oh My Grub](./03-Oh-My-Grub.md) | Forensics | Easy | ✅ |

---

## 🗺️ Patterns Recognized

| Pattern | First Seen In |
|---------|--------------|
| Deleted files persist on FAT filesystems until overwritten | Deleted File |
| Image metadata can contain hidden or meaningful information | Deleted File |
| Visual inspection alone is insufficient — always check metadata | Deleted File |
| Memory dumps can be triaged with basic tools before specialized frameworks | Command & Control - Level 2 |
| The same artifact can exist in multiple locations within a memory dump | Command & Control - Level 2 |
| Environment variable blocks in memory expose system configuration data | Command & Control - Level 2 |
| Virtual disk images require dedicated mounting tools, not raw extraction | Oh My Grub |
| Permission errors during forensic mounting are configuration problems, not dead ends | Oh My Grub |
| Hidden files must be enumerated as a standard step, not a last resort | Oh My Grub |

---

## 📈 Skills Gained So Far

- **FAT Filesystem Forensics** — Understanding how file deletion works at the filesystem level and why data recovery is possible
- **File Carving** — Using signature-based tools to recover files from raw disk images without a filesystem index
- **Metadata Analysis** — Extracting and interpreting embedded metadata from image files as part of a forensic investigation
- **Memory Dump Triage** — Applying `strings` and `grep` as a first-pass method to extract readable artifacts from raw binary memory dumps
- **Windows System Artifact Analysis** — Understanding where Windows stores hostname and environment data in memory, and how to locate it under forensic conditions
- **Investigative Pivoting** — Recognizing when an approach returns noise and redirecting to alternative data sources within the same file
- **Virtual Disk Forensics** — Mounting `.vmdk` images safely in read-only mode using inspection tools and navigating the recovered filesystem as a live evidence source

---

## 📖 Resources That Helped Me

- [Root-Me Forensics Challenges](https://www.root-me.org/)
- [ExifTool Documentation](https://exiftool.org/)
- [Foremost File Carver](http://foremost.sourceforge.net/)

---

## 🔗 Related Repo

This forensics repo runs in parallel with my networking CTF documentation:
👉 [CTF Networking — Root-Me](https://github.com/RYO-1313/CTF-Networking-Root-Me)

Both repositories follow the same documentation philosophy and target the same career objective: SOC Analyst → Red Team.

---

*This repository is a living document. Every challenge completed, every mistake made, and every concept learned is recorded here — not just to track progress, but to build the analytical habits that matter in a professional security environment.*
