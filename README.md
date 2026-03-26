# 🔬 CTF Forensics — Root-Me

> *Documenting a self-taught journey through forensics challenges on Root-Me, with a focus on building SOC Analyst fundamentals and analytical methodology.*

---

## 👤 About Me

Self-taught cybersecurity student targeting a career as a **SOC Analyst**, with a long-term goal of transitioning into Red Team operations. I practice daily on Root-Me and TryHackMe (Blue Team pathways), and document every challenge to reinforce learning and build a professional portfolio.

- 🐧 Daily Linux user (CachyOS + Kali Linux VM)
- 🔵 TryHackMe — Blue Team pathways
- 🌐 Parallel repo: [CTF Networking — Root-Me](https://github.com/RYO-1313/CTF-Networking-Root-Me)

---

## 🧰 Tools Used

| Tool | Purpose |
|------|---------|
| `file` | File type identification and initial recon |
| `foremost` | File carving and recovery from raw disk images |
| `binwalk` | Embedded file signature detection in binary images |
| `exiftool` | Metadata extraction and analysis from media files |

---

## 📚 Challenges Completed

| # | Challenge | Category | Difficulty | Status |
|---|-----------|----------|------------|--------|
| 01 | [Deleted File](./01-Deleted-File.md) | Forensics | Very Easy | ✅ |

---

## 🗺️ Patterns Recognized

| Pattern | First Seen In |
|---------|--------------|
| Deleted files persist on FAT filesystems until overwritten | Deleted File |
| Image metadata can contain hidden or meaningful information | Deleted File |
| Visual inspection alone is insufficient — always check metadata | Deleted File |

---

## 📈 Skills Gained So Far

- **FAT Filesystem Forensics** — Understanding how file deletion works at the filesystem level and why data recovery is possible
- **File Carving** — Using signature-based tools to recover files from raw disk images without a filesystem index
- **Metadata Analysis** — Extracting and interpreting embedded metadata from image files as part of a forensic investigation

---

## 📖 Resources That Helped Me

- [Root-Me Forensics Challenges](https://www.root-me.org/en/Challenges/Forensic/)
- [ExifTool Documentation](https://exiftool.org/)
- [Foremost File Carver](http://foremost.sourceforge.net/)

---

## 🔗 Related Repo

This forensics repo runs in parallel with my networking CTF documentation:

👉 [CTF Networking — Root-Me](https://github.com/RYO-1313/CTF-Networking-Root-Me)

Both repositories follow the same documentation philosophy and target the same career objective: **SOC Analyst → Red Team**.

---

*This repository is a living document. Every challenge completed, every mistake made, and every concept learned is recorded here — not just to track progress, but to build the analytical habits that matter in a professional security environment.*
