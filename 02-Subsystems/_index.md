# Subsystems

> "You don't contribute to the kernel.
> You contribute to a subsystem.
> Pick one. Go deep."

---

## What is a subsystem?

A subsystem is a major folder in the kernel repo.
Each one is an independent project with its own
maintainer, mailing list, and contributor community.

---

## 🟢 Beginner Friendly

Best place to start. Low barrier to entry.
Good for first patches.

| Subsystem | What it does |
|-----------|-------------|
| [[init/_index\|init/]] | First code after boot |
| [[Documentation/_index\|Documentation/]] | Official docs — best first patch target |
| [[samples/_index\|samples/]] | Example kernel code |
| [[scripts/_index\|scripts/]] | Build and analysis tools |
| [[tools/_index\|tools/]] | Userspace developer tools |

---

## 🟡 Intermediate

Understand basic kernel concepts first.
Processes, memory, syscalls minimum.

| Subsystem | What it does |
|-----------|-------------|
| [[kernel/_index\|kernel/]] | Core — scheduling, signals, timers |
| [[fs/_index\|fs/]] | Filesystem layer |
| [[ipc/_index\|ipc/]] | Inter-process communication |
| [[security/_index\|security/]] | SELinux, AppArmor, LSM |
| [[crypto/_index\|crypto/]] | Encryption primitives |
| [[block/_index\|block/]] | Block device layer |
| [[lib/_index\|lib/]] | Shared utilities |

---

## 🔴 Advanced

Serious study needed before contributing.

| Subsystem | What it does |
|-----------|-------------|
| [[net/_index\|net/]] | TCP/IP stack, networking |
| [[drivers/_index\|drivers/]] | Hardware drivers |
| [[arch/_index\|arch/]] | CPU architecture specific |
| [[sound/_index\|sound/]] | Audio subsystems |
| [[virt/_index\|virt/]] | Virtualization, KVM |
| [[io_uring/_index\|io_uring/]] | Modern async I/O |

---

## ⚫ Wizard Territory

Don't start here.
Even experienced developers find these hard.

| Subsystem | What it does |
|-----------|-------------|
| [[mm/_index\|mm/]] | Memory management |
| [[arch/_index\|arch/]] | Deep architecture internals |

---

## 🆕 Modern — Less Documented

Newer additions. Less existing documentation.
High opportunity for contributors.

| Subsystem | What it does |
|-----------|-------------|
| [[rust/_index\|rust/]] | Rust support — growing fast |
| [[io_uring/_index\|io_uring/]] | Modern async I/O |

---

## Don't know which to pick?


Want first patch fast? → [[Documentation/_index|Documentation/]]

Interested in how files work? → [[fs/_index|fs/]]

Interested in networking? → [[net/_index|net/]]

Interested in hardware? → [[drivers/_index|drivers/]]

Interested in Rust in kernel? → [[rust/_index|rust/]]

Just want a map first? → [[01-Root-Overview/_index|Back to Root Overview]]


---

## Next

Pick a subsystem above and dive in.
Or follow a structured path:
→ [[05-Contributor-Paths/_index|Contributor Paths]]
