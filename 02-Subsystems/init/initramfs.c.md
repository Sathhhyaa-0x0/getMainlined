---
title: initramfs.c
---
# initramfs.c

🟢 Beginner Friendly

Part of [[_index|init/]]

---
## What is this file?

initramfs.c handles loading and unpacking the
initial RAM filesystem — a temporary filesystem
that lives entirely in memory during early boot.

Before your real filesystem on your SSD or
hard drive gets mounted, the kernel needs
certain tools and drivers to even find and
access that storage. initramfs provides those
tools temporarily.

---
## The chicken and egg problem it solves

Here's the problem Linux boot faces:

To mount your real root filesystem
you might need a storage driver.

But drivers live on your root filesystem.

So how do you load the driver before
you can access the filesystem that
contains the driver?

initramfs solves this completely by providing temporary tools.

---
### Boot sequence with initramfs:

```
Bootloader loads kernel + initramfs into RAM
↓
initramfs unpacked into memory 			
↓
Temporary filesystem available immediately 
↓
Kernel loads drivers from initramfs
↓
Real root filesystem found and mounted
↓
initramfs discarded from memory 
↓
System continues from real filesystem
```


---
## What initramfs contains

A typical initramfs contains:

essential storage drivers
filesystem drivers
tools like mount and switch_root
udev for device detection
sometimes cryptsetup for encrypted drives
sometimes LVM tools for logical volumes

All of this lives in a small compressed
archive that the bootloader loads alongside
the kernel itself.

---
## initramfs vs initrd

These terms confuse almost every beginner.

initrd — older method. An actual block device
image mounted as a RAM disk. Still supported
for compatibility. Handled by do_mounts_initrd.c

initramfs — modern method. A cpio archive
unpacked directly into a tmpfs. Simpler,
faster, more flexible. What almost all
modern Linux systems use.

initramfs.c handles the modern initramfs path.
do_mounts_initrd.c handles the legacy initrd path.

---
## What this file specifically does

initramfs.c unpacks the cpio archive that
the bootloader loaded into memory. It reads
the archive format, creates the directory
structure, and places all the files into
the temporary in-memory filesystem.

After unpacking it hands control to the
init program inside the initramfs — usually
a shell script or small binary that does
the actual driver loading and filesystem
mounting before switching to the real root.

---
## Contributor angle

Good for first contribution? Yes carefully.

The file has decent comments but the
logic is non-trivial. Documentation
improvements are the safest entry point.

There is active work around initramfs
in modern kernels — compressed formats,
performance improvements. Worth watching
for opportunities.

Mailing list → linux-kernel@vger.kernel.org

---
## Connects to

[[do_mounts.c]] — coordinates with initramfs
to decide the final root mount path.

[[02-Subsystems/fs/_index|fs/]] — the tmpfs
filesystem that initramfs unpacks into.

[[main.c]] — early boot calls initramfs
unpacking before do_mounts runs.

[[04-Execution-Journeys/_index|Boot Journey]]
— see exactly where initramfs fits in
the complete boot sequence.

---
## Beginner confusion this clears

Many beginners see initramfs and think
it's some kind of optional feature or
emergency recovery tool.

It's neither. On almost every modern
Linux system it's a mandatory part of
the boot process. Your system very likely
cannot boot without it.

Run this on any Linux system:

ls /boot/

You'll see a file called initramfs or
initrd.img alongside the kernel. That
file is what this code unpacks.

---

→ [[calibrate.c]] — read this next
→ [[_index|Back to init/]]