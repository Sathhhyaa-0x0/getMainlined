---
title: calibrate.c 
---
# calibrate.c

🟢 Beginner Friendly

Part of [[07-Meta/_index|init/]]

---
## What is this file?

calibrate.c measures how fast the CPU is
at boot time by counting how many iterations
of a simple loop fit inside a known time window.

The result gets stored as loops_per_jiffy —
a value the kernel uses whenever it needs
to create a short busy-wait delay.

---
## Why the kernel needs this

Sometimes the kernel needs to wait for a
very short time — nanoseconds to microseconds.
Too short for a proper sleep. The only option
is a busy loop that just burns CPU cycles.

But how many loop iterations equal one
microsecond on this specific CPU?

That depends entirely on the hardware.
A slow embedded CPU and a fast desktop CPU
give completely different answers.

calibrate.c figures out the answer at boot
by actually measuring it on the real hardware
rather than hardcoding any assumption.

---
## How it works

The logic is surprisingly simple:
```

Start with a guess for loops_per_jiffy ↓ Run a loop for that many iterations ↓ Check how much real time passed ↓ Too fast? Double the count Too slow? Adjust down ↓ Repeat until the loop takes exactly one jiffy of time ↓ Store the result as loops_per_jiffy

```

That's it. No complex math. Just
iterative measurement and adjustment.

---
## What you see at boot

When Linux boots you sometimes see:

Calibrating delay loop... 4200.00 BogoMIPS

BogoMIPS means Bogus MIPS. Linus himself
named it this. It's not a real performance
measurement — just a rough indicator of
how fast the CPU can execute a simple loop.

The BogoMIPS value comes directly from
the loops_per_jiffy result in this file.

---
## Why read this file first

calibrate.c is arguably the most beginner
friendly file in the entire kernel for
one specific reason:

The core logic is pure C with no kernel
specific concepts. No locking. No memory
management. No complex data structures.

Just a loop, a timer check, and some
arithmetic. A beginner who knows basic C
can read and understand the core logic
completely on their first attempt.

Open it on GitHub right now and read it.
You'll understand more than you expect.

---
## Contributor angle

Good for first contribution? Limited.

The file is small, stable, and rarely
needs changes. Maintainers would question
most modifications here.

Better to read it for understanding
than target it for contribution.

Its real value is as your first kernel
source file to actually read and understand
completely end to end.

---
## Connects to

[[main.c]] — calibrate_delay() is called
from start_kernel() during early boot.

[[02-Subsystems/kernel/_index|kernel/]] —
the jiffy timing system that calibrate.c
measures against lives here.

---
## Beginner confusion this clears

BogoMIPS sounds like a real benchmark.
It isn't. Linus literally called it bogus.

It's just loops_per_jiffy scaled to a
human readable number. Different kernels,
different compiler optimizations, different
loop bodies — all give different BogoMIPS
on the same hardware.

Never use it to compare CPU performance.
It measures one specific loop. Nothing more.

---
→ [[version.c]] — read this next
→ [[07-Meta/_index|Back to init/]]