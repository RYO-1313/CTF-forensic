# 🛡️ Command & Control - Level 2 — Root-Me Writeup

**Platform:** Root-Me
**Category:** Forensics
**Difficulty:** Easy
**Status:** ✅ Completed

---

## 🔍 What the Challenge Was

A memory dump (`ch2.dmp`) was provided from a compromised workstation. The objective was to recover the machine's hostname — a piece of information that had been lost during the incident response process. The flag was the workstation's hostname itself.

---

## 🧠 What I Learned

This was my first memory forensics challenge, and the entire methodology was new territory. I had no prior experience working with raw memory dumps, so every step required building understanding from scratch — from identifying the file type, to understanding where Windows stores system information, to navigating the noise that a memory dump produces.

The moment that brought clarity was pivoting from searching for registry key names to searching for `WORKGROUP` — a Windows default network identifier. That search revealed environment variable blocks embedded in memory, which consistently contained the hostname alongside them. It reframed how I think about memory: the same piece of information can exist in multiple locations within a dump, and when one path is noisy or incomplete, the correct response is to pivot and look elsewhere.

---

## 🛠️ My Approach

The investigation began with basic file identification using the `file` command, which returned "data" — confirming a raw binary with no recognizable format header, consistent with a memory dump.

Rather than immediately reaching for a specialized forensics framework, I applied `strings` to extract all human-readable content from the binary. This produced a large volume of output, which was then filtered using `grep` to search for patterns associated with Windows hostname storage.

Initial attempts targeted `ComputerName` and `ActiveComputerName` — the registry keys Windows uses to store the machine name under `SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`. While the registry path was present in the output, the actual hostname value was not cleanly recoverable from that location due to encoding in memory.

The successful approach came from searching for `WORKGROUP` — the Windows default workgroup identifier — which surfaced environment variable blocks embedded in the dump. These blocks contained a consistent, structured snapshot of the system environment, including the hostname. Cross-referencing multiple occurrences of this pattern confirmed the hostname with high confidence.

---

## 💡 Key Skill Learned

**Memory artifact analysis without specialized tooling** — using `strings` and `grep` as a first-pass triage method on raw binary files. Before reaching for advanced frameworks, readable artifacts can often be extracted with basic command-line tools. Knowing *where* Windows stores system information (registry, environment variables, process memory) guides the search effectively.

---

## 🔑 Core Takeaway

In memory forensics, the same data point can exist in multiple locations within a dump. The registry is not always the cleanest source. When a structured approach returns noise, pivoting to adjacent data — such as environment variable blocks — can surface the same information in a more readable form. Flexibility in methodology is as important as technical knowledge.

---

## 🤖 Claude's Role

Claude guided the investigative process without providing direct answers. It introduced the concept of Windows hostname storage locations, explained the purpose of each command-line tool as it was introduced, and prompted pivots when initial approaches returned inconclusive results. The identification of the hostname and the decision-making throughout the process remained with me.
