---
title: do_mounts.c
---
# do_mounts.c

🟢 Beginner Friendly

Part of [[_index|init/]]

---
## What is this file?

do_mounts.c handles mounting the root filesystem
during boot. This is the moment Linux can actually
read your hard drive for the first time.

Before this file runs — the kernel exists only
in memory. No files. No filesystem. Nothing
persistent. After this file runs — the kernel
has access to your actual storage.

---
## Why it matters

Every Linux system needs a root filesystem.
Without it there is nowhere to find userspace
programs, configuration files, or anything else
the system needs to run.

do_mounts.c is responsible for finding that
root filesystem and making it available.
It's the bridge between the kernel living
purely in memory and the kernel having
access to persistent storage.

---
## What it actually does

The kernel needs to know where the root
filesystem lives. This information comes
from the bootloader — usually as a kernel
command line parameter like:

root=/dev/sda1
root=UUID=xxxx-xxxx
root=/dev/mmcblk0p2

do_mounts.c reads that parameter, finds
the right block device, and mounts it
as the root filesystem at /.

If it fails — kernel panic. No root
filesystem means the system cannot continue.

---
## The mounting sequence

do_mounts.c doesn't work alone. It coordinates
with several other files in init/:

do_mounts_initrd.c handles the legacy path
where an initial RAM disk was used before
the real filesystem mounts.

do_mounts_rd.c handles the case where root
is on a RAM disk entirely.

noinitramfs.c handles the case where no
initial RAM filesystem exists at all.

do_mounts.c is the coordinator that decides
which path to take based on what the
bootloader passed in.

---
## Kernel panic you've probably seen

"VFS: Unable to mount root fs on unknown block"

That error comes from this file. It means
do_mounts.c couldn't find or mount the
root filesystem. Common causes:

wrong root= parameter passed by bootloader
missing driver for the storage device
corrupted filesystem

---
## Contributor angle

Good for first contribution? Possibly.

This file is moderately complex but
well commented. Documentation improvements
and comment clarifications are welcome.

Mailing list → linux-kernel@vger.kernel.org

---
## Connects to

[[main.c]] — do_mounts is called during
the boot sequence started by start_kernel().

[[02-Subsystems/fs/_index|fs/]] — the VFS (Virtual File System)
layer that actually handles the mount
operation lives here.

[[02-Subsystems/block/_index|block/]] — the
block device layer that do_mounts talks to
when finding the root device.

[[04-Execution-Journeys/_index|Boot Journey]]
— see exactly where do_mounts fits in
the full boot sequence.

---
## Beginner confusion this clears

Many beginners think Linux just "finds"
the filesystem automatically. It doesn't.

The bootloader explicitly tells the kernel
where root is via the root= parameter.
do_mounts.c reads that instruction and
acts on it. Nothing magical — just
careful parameter parsing and device lookup.

---

→ [[initramfs.c]] — read this next
→ [[_index|Back to init/]]