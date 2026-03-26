# 🛡️ Deleted File — Root-Me Writeup

**Platform:** Root-Me
**Category:** Forensics
**Difficulty:** Very Easy

---

## 🔍 What the challenge was

A raw FAT16 USB disk image was provided. A file had been deleted from it, and the goal was to recover it and extract meaningful information from it.

---

## 🧠 What I learned

- When a file is deleted on a FAT filesystem, only the directory entry pointer is removed — the actual data blocks remain on disk until overwritten. This makes recovery possible with the right tools.
- How to use **foremost** to carve and recover deleted files from a raw disk image based on file signatures.
- How to use **exiftool** to read metadata embedded inside image files — including fields like Creator, timestamps, GPS, and comments that are invisible when simply viewing the image.

---

## 🛠️ My Approach

1. Ran `file` on the disk image to identify it as a FAT16 filesystem — a raw USB drive image.
2. Recognized that deleted files may still exist in the raw data and used **foremost** to carve recoverable files from the image.
3. Foremost successfully recovered a PNG image — a photo of a tree.
4. Rather than stopping at the visual content, applied **exiftool** to inspect the image's embedded metadata.
5. Discovered a `Creator` field in the metadata containing the flag.

*Note: binwalk was also run during recon and confirmed the presence of a PNG at a specific offset, but foremost handled the full extraction.*

---

## 💡 Key Skill Learned/Reinforced

Using **exiftool** to go beyond what is visible in an image — metadata analysis as a core forensics technique for recovering hidden or overlooked information embedded in files.

---

## 🔑 Core Takeaway

Forensics is not just about what you can see. A file that appears to be a simple photo can carry hidden information in its metadata. The investigation does not end at visual inspection — it ends when every layer of the file has been examined.

---

## 🤖 Claude's Role

Provided conceptual guidance on FAT filesystem deletion mechanics and hinted toward the correct tooling when I was uncertain. All tool execution, analysis, and flag discovery were performed independently.
