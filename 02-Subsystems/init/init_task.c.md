---
title: init_task.c
---
# init_task.c

🟢 Beginner Friendly

Part of [[_index|init/]]

---
## What is this file?

init_task.c defines the very first task in the
entire Linux kernel. This is PID 0 — the idle task.

Every single process that will ever run on your
system is a descendant of this task. It is the
ancestor of all processes, created not dynamically
like everything else but statically at compile time.

---
## Why it matters

Most things in Linux are created at runtime.
init_task is different — it is hardcoded into
the kernel binary itself. It exists before
memory management is even initialized.

When start_kernel() begins running in main.c,
init_task is already there. It's the context
the kernel runs in during early boot before
any real process exists.

---
## PID 0 vs PID 1 — the confusion

PID 0 — init_task — the idle task.
Lives in kernel space forever.
Runs when no other process needs the CPU.
Never visible in ps or top.
Defined right here in this file.

PID 1 — the init process.
Created by rest_init() in main.c.
Becomes systemd or /sbin/init.
Visible in ps as the first userspace process.
Parent of all userspace processes.

Two very different things.
Both called "init" in different contexts.
This file is only about PID 0.

---
## Contributor angle

Good for first contribution? Not really.

This file is tiny and rarely touched.
Very few reasons to change it.
Maintainers would question why you're here.

Better to read it for understanding
than to contribute to it directly.

---
## Connects to

[[main.c]] — start_kernel() runs in the
context of init_task.

[[02-Subsystems/kernel/_index|kernel/]] — the
scheduler knows about init_task specially.

[[04-Execution-Journeys/_index|Boot Journey]]
— init_task is the starting point of the
entire boot execution context.

---
## Beginner confusion this clears

Many beginners assume PID 1 is the first thing
the kernel creates. It's not.

PID 0 exists before PID 1. Before memory
management. Before the scheduler. Before
almost everything.

init_task is the silent foundation everything
else is built on top of.

---

→ [[do_mounts.c]] — read this next
→ [[_index|Back to init/]]