# 🛡️ Oh My Grub — Root-Me Writeup

**Platform:** Root-Me
**Category:** Forensics
**Difficulty:** Easy

---

## 🔍 What the challenge was

A company lost access to an old server containing important files. The objective was to recover those files from a provided `.ova` archive — a virtual machine package containing the disk image of the target system.

---

## 🧠 What I learned

- An `.ova` file is a tar archive that packages a virtual machine — extracting it reveals the `.ovf` configuration file and the `.vmdk` virtual disk image that holds the actual data
- Virtual disk images require dedicated mounting tools rather than standard Linux mount commands — `guestmount` can inspect and map a VMDK to a local directory without requiring manual partition identification
- The `-o allow_other` flag in `guestmount` is necessary to bypass FUSE permission restrictions that would otherwise deny access to the mounted filesystem from a privileged shell
- Privilege escalation on the host side was required to navigate the mounted filesystem — standard user permissions were insufficient due to Linux DAC enforcement
- Critical files on a target system are not always in obvious locations — I initially searched the wrong directory before correctly pivoting to the system administrator's home directory
- Hidden files exist outside the default view of directory listings — a habit of running a full directory listing including hidden entries is necessary to avoid missing evidence

---

## 🛠️ My Approach

The investigation began with identifying the `.ova` file as a POSIX tar archive and extracting its contents, which revealed the VM configuration file and the virtual disk image. After confirming the disk image format, the focus shifted to accessing the filesystem inside it.

Rather than attempting raw carving, the disk was mounted using `guestmount` in read-only inspection mode, mapping it to a local directory on the analysis host. Initial access was blocked by FUSE permission restrictions, which was resolved by appending the `allow_other` flag to the mount command and operating from a root shell.

Navigation through the mounted filesystem revealed that the target files were not located in the user's home directory as initially assumed. Redirecting to the system administrator's directory and running a full directory listing — including hidden entries — uncovered a concealed credential file containing the flag.

---

## 💡 Key Skill Learned / Reinforced

**Virtual Disk Forensics** — Understanding how to treat a `.vmdk` as a forensic artifact, mount it safely in read-only mode using inspection tools, and navigate the recovered filesystem as a live evidence source rather than relying on raw extraction methods.

---

## 🔑 Core Takeaway

Permission errors during forensic mounting are not dead ends — they are configuration problems with known solutions. More importantly, a thorough investigation requires checking for hidden files as a standard step, not as a last resort. Evidence that is not immediately visible is not evidence that does not exist.

---

## 🤖 Claude's Role

Claude's involvement in this challenge was limited to writeup documentation only. The investigation, tooling decisions, and problem-solving were carried out independently.
