# main.c

🟢 Beginner Friendly — but deeply important

Part of [[_index|init/]]

---

## What is this file?

main.c is the entry point of the Linux kernel.

After the bootloader loads the kernel into memory
and hands over control, execution eventually reaches
start_kernel() — which lives in this file.

Everything starts here. Every subsystem, every
driver, every data structure the kernel needs
to function — all initialized from this one function.

If the kernel were a human body, start_kernel()
is the moment the heart beats for the first time.

---

## Why it matters

This is the single most important file to read
as a beginner. Not because it's complex —
but because it gives you the complete picture
of how Linux wakes up.

Reading start_kernel() top to bottom tells you
every major subsystem that exists and roughly
what order they initialize. It's an index of
the entire kernel disguised as a function.

---

## Key function

start_kernel()

This is what you're here for. It's a long
function that calls initialization routines
one by one. Some examples of what it calls:

setup_arch() — architecture specific setup
mm_init() — memory management initialization
sched_init() — scheduler initialization
vfs_caches_init() — filesystem cache setup
rest_init() — starts the first real process

Each of those calls leads into a different
subsystem. Follow any one of them and you're
reading a different part of the kernel.

---

## rest_init() — the handoff

At the very end of start_kernel() comes
rest_init(). This is where the kernel creates
the first real userspace process — PID 1.

That process becomes systemd or /sbin/init
on your running system. The kernel's job after
this point shifts from initialization to
managing processes that are already running.

---

## How to read this file

Don't try to understand every line.

First pass — just read the function names
inside start_kernel(). Each name tells you
what subsystem is initializing. You're building
a mental map, not memorizing code.

Second pass — pick one function call that
interests you and follow it into its subsystem.
That's how kernel reading works. You pull
one thread and follow it.

---

## Contributor angle

Good for first contribution? Carefully yes.

main.c is heavily reviewed. Every line
has been touched by Linus himself. Standards
are extremely high here.

Best contribution type → comment improvements,
documentation fixes, nothing structural.

Don't try to change start_kernel() logic
as a first patch. You will get rejected
and it will hurt. 😄

---

## Connects to

[[02-Subsystems/mm/_index|mm/]] — mm_init() is
called from start_kernel(). Memory management
wakes up here.

[[02-Subsystems/kernel/_index|kernel/]] — sched_init()
starts the scheduler from here.

[[02-Subsystems/fs/_index|fs/]] — vfs_caches_init()
initializes the filesystem layer from here.

[[init_task.c]] — the first task structure that
exists before start_kernel() even runs.

[[04-Execution-Journeys/_index|Boot Journey]] —
see the full sequence start_kernel() triggers.

---

## Beginner confusion this clears

Many beginners think the kernel just "starts."
main.c shows that startup is a carefully
ordered sequence of subsystem initializations.

Each subsystem depends on the one before it.
Memory must exist before the scheduler.
The scheduler must exist before processes.
Processes must exist before filesystems mount.

That order is visible right here in
start_kernel() if you read it carefully.

---

→ [[init_task.c]] — read this next
→ [[_index|Back to init/]]