# Linux Kernel Repo — Root Overview

> "You opened torvalds/linux. 
> Here's what you're looking at."
> Link: https://github.com/torvalds/linux/tree/master

---
## What is this repo?

This is the actual source code of the Linux kernel
maintained by Linus Torvalds himself.

Every line here runs on:
- 97% of the world's servers
- Every Android phone
- NASA systems
- Stock exchanges
- Probably the device you're reading this on

---
## The folders

### 🟢 Start here — easiest to understand

| Folder                                                 | What it does                                          |
| ------------------------------------------------------ | ----------------------------------------------------- |
| [[02-Subsystems/Documentation/_index\|Documentation/]] | Official kernel docs. Also your first patch target.   |
| [[02-Subsystems/init/_index\|init/]]                   | First code that runs after boot. Where it all begins. |
| [[02-Subsystems/samples/_index\|samples/]]             | Example kernel code. Safe to read.                    |
| [[02-Subsystems/scripts/_index\|scripts/]]             | Build and analysis tools. checkpatch.pl lives here.   |
| [[02-Subsystems/tools/_index\|tools/]]                 | Userspace tools for kernel developers.                |
| [[02-Subsystems/LICENSES/_index\|LICENSES/]]           | License files. Nothing technical.                     |

---

### 🟡 Core kernel behavior

| Folder | What it does |
|--------|-------------|
| [[02-Subsystems/kernel/_index\|kernel/]] | Scheduling, signals, timers. The boss of the OS. |
| [[02-Subsystems/ipc/_index\|ipc/]] | Inter-process communication. Pipes, shared memory. |
| [[02-Subsystems/security/_index\|security/]] | SELinux, AppArmor, kernel security framework. |
| [[02-Subsystems/crypto/_index\|crypto/]] | Encryption primitives used across the kernel. |
| [[02-Subsystems/lib/_index\|lib/]] | Shared utility functions used everywhere. |

---

### 🟡 Filesystem and storage

| Folder | What it does |
|--------|-------------|
| [[02-Subsystems/fs/_index\|fs/]] | ext4, btrfs, FAT — how files are stored and accessed. |
| [[02-Subsystems/block/_index\|block/]] | Block device layer. Between filesystem and hardware. |
| [[02-Subsystems/io_uring/_index\|io_uring/]] | Modern async I/O. Very active, hot topic right now. |

---

### 🟡 Networking

| Folder | What it does |
|--------|-------------|
| [[02-Subsystems/net/_index\|net/]] | TCP/IP stack, sockets, all network protocols. |

---

### 🔴 Hardware and drivers

| Folder | What it does |
|--------|-------------|
| [[02-Subsystems/drivers/_index\|drivers/]] | Everything from USB to GPUs. 50% of the entire repo. |
| [[02-Subsystems/arch/_index\|arch/]] | CPU specific code. x86, ARM, RISC-V live here. |
| [[02-Subsystems/sound/_index\|sound/]] | Audio subsystems and drivers. |
| [[02-Subsystems/virt/_index\|virt/]] | Virtualization support. KVM lives here. |

---

### ⚫ Wizard territory

| Folder | What it does |
|--------|-------------|
| [[02-Subsystems/mm/_index\|mm/]] | Memory management. Page allocation, virtual memory, OOM killer. |

---

### 🆕 Modern additions

| Folder | What it does |
|--------|-------------|
| [[02-Subsystems/rust/_index\|rust/]] | Rust language support. Added 2022. Growing fast. |
| [[02-Subsystems/certs/_index\|certs/]] | Kernel certificates and signing. |

---

## The root files

These aren't folders — they're files sitting
at the root level. Beginners always wonder
what these do.

| File | What it does |
|------|-------------|
| [[03-Key-Files/Makefile\|Makefile]] | How to build the kernel. Entry point for compilation. |
| [[03-Key-Files/Kconfig\|Kconfig]] | Configuration system. What gets compiled in or out. |
| [[03-Key-Files/Kbuild\|Kbuild]] | Build system rules used across the whole tree. |
| [[03-Key-Files/MAINTAINERS\|MAINTAINERS]] | Who owns what subsystem. Use this to find who reviews your patch. |
| [[03-Key-Files/CREDITS\|CREDITS]] | Historical contributors. Your name could be here someday. |
| README | Basic intro. Surprisingly minimal for such a huge project. |
| COPYING | GPL v2 license. Everything here is open source. |

---

## The most important thing to understand

This repo is not one project. It's 30+ independent subsystems living under one roof.

Each subsystem has: → Its own maintainer → Its own mailing list → Its own standards → Its own contributor community

You don't contribute to "the kernel." You contribute to a subsystem. Pick one. Go deep.


---
## What connects to what


User types: open("file.txt") ↓ [[02-Subsystems/kernel/_index|kernel/]] (syscall handling) ↓ [[02-Subsystems/fs/_index|fs/]] (VFS layer) ↓ [[02-Subsystems/block/_index|block/]] (block device layer) ↓ [[02-Subsystems/drivers/_index|drivers/]] (actual hardware driver) ↓ Your SSD


This is a preview of what Execution Journeys
covers in full detail.

---

## Where to go from here

Picked a subsystem that interests you?
→ [[02-Subsystems/_index|Browse all subsystems]]

Want your first patch?
→ [[05-Contributor-Paths/_index|Contributor Paths]]

Unfamiliar with a concept?
→ [[06-Concepts/_index|Concepts]]