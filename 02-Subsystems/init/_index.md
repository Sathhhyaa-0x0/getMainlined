# init/

Link: https://github.com/torvalds/linux/tree/master/init

🟢 Beginner Friendly

This is where the kernel begins. After the bootloader
hands control to the kernel, init/ is the first
directory that matters.

start_kernel() lives here. Every subsystem
initialization, every data structure setup,
every driver probe — all triggered from this
single function.

If you want to understand how Linux goes from
"just loaded into memory" to "fully running OS"
— this is your starting point.

---

## Key Files

These are the files worth reading deeply.
Each has its own dedicated note.

[[main.c]] — The most important file in the entire
kernel. start_kernel() lives here. Every subsystem
boots from this single function. Read this first.

[[init_task.c]] — Defines the very first task the
kernel creates. PID 0. The ancestor of every single
process that will ever run on the system.

[[do_mounts.c]] — Handles mounting the root
filesystem. The moment Linux can actually read
your hard drive for the first time.

[[initramfs.c]] — Loads and unpacks the initramfs
image. The temporary filesystem loaded into memory
before the real root filesystem is mounted.

[[calibrate.c]] — Measures CPU speed at boot
by counting how many loops fit in a known
time window. Simple and very readable.
Good first file for a beginner to open.

[[version.c]] — Generates the kernel version
string you see when you run uname -r.
Simplest file in init/. Good starting read.

---

## All Other Files

Every file explained so nothing is a mystery.

[[do_mounts.h]] — Header file for do_mounts.c.
Declares the functions and structures used
across the mount related files.

[[do_mounts_initrd.c]] — Handles the legacy initrd
mounting path. Older method before initramfs
existed. Mostly maintained for compatibility.

[[do_mounts_rd.c]] — Handles RAM disk mounting
specifically. Used when root filesystem lives
on a RAM disk.

[[noinitramfs.c]] — Fallback used when no
initramfs is provided at boot. Minimal stub
that handles the no initramfs case cleanly.

[[initramfs_internal.h]] — Internal header for
initramfs. Not meant to be used outside init/.
Declares internal structures.

[[initramfs_test.c]] — Unit tests for initramfs
unpacking logic. Good example of how kernel
unit tests are written.

[[version-timestamp.c]] — Records the timestamp
of when the kernel was built. Used in the
version string alongside version.c.

[[Kconfig]] — Configuration options for init/.
Controls what features get compiled in.
Read this to understand what is optional.

[[Makefile]] — Build rules for init/.
Tells the build system which files to compile
and under what conditions.

[[.gitignore]] — Lists files that git should
ignore in this directory. Not kernel code —
just build system housekeeping.

[[.kunitconfig]] — Configuration for KUnit
tests in init/. Used when running kernel
unit tests locally.

---

## Why it exists

The kernel needs a defined entry point after boot.
init/ provides that. Without it there's no starting
point — just code sitting in memory with nothing
telling it where to begin.

---

## Contributor angle

Good for beginners? Yes — but careful.
init/ is small and clean which means
maintainers have high standards here.

Best contribution type → documentation
improvements, comment clarifications,
cleanup patches.

Mailing list → linux-kernel@vger.kernel.org

---

## Connects to

[[02-Subsystems/mm/_index|mm/]] — memory management
initializes during boot sequence.

[[02-Subsystems/kernel/_index|kernel/]] — core kernel
subsystems start here.

[[02-Subsystems/fs/_index|fs/]] — root filesystem
gets mounted from init/.

[[04-Execution-Journeys/_index|Execution Journeys]]
— see the full boot journey.

---

## Beginner confusion this clears

init/ is NOT the init process (PID 1).
That's /sbin/init or systemd in userspace.

init/ in the kernel repo is the kernel's
own initialization code. Two completely
different things sharing a confusing name.

---

→ [[main.c]] — read this next
→ [[02-Subsystems/_index|Back to Subsystems]]