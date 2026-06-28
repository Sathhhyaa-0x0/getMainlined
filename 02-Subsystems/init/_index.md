---
title: init
---
# init/

Link: [https://github.com/torvalds/linux/tree/master/init](https://github.com/torvalds/linux/tree/master/init)

🟢 Beginner Friendly

This subsystem contains the generic initialization  
path of the Linux kernel.

CPU execution begins earlier in architecture-specific  
startup code, but eventually control reaches init/  
where the kernel begins building the world it needs  
to run.

Memory initialization.  
Scheduler startup.  
Filesystem preparation.  
Process creation.

If you want to understand how Linux goes from  
"loaded into memory" to "running operating system"  
— start here.

---
## What this subsystem does

Bootloader  
↓  
Architecture startup  
↓  
start_kernel()  
↓  
Subsystem initialization  
↓  
rest_init()  
↓  
kernel_init()  
↓  
Userspace

This directory coordinates that transition.

---
## Read in this order

### Tier 0 — Orientation

Read first. Build a mental map.

→ [[04-Execution-Journeys/_index|Boot Journey]]

---

### Tier 1 — Landmark files

Read deeply.

[[main.c]]  
The most important file in init/.  
Contains start_kernel().

[[init_task.c]]  
Defines the earliest task structures.

---

### Tier 2 — Core implementation

Understand mechanisms.

[[do_mounts.c]]  
Mounting the root filesystem.

[[initramfs.c]]  
Loading temporary boot filesystem.

[[calibrate.c]]  
Boot-time CPU calibration.

---

### Tier 3 — Supporting files

Reference when needed.

[[version.c]]  
[[do_mounts.h]]  
[[do_mounts_initrd.c]]  
[[do_mounts_rd.c]]  
[[noinitramfs.c]]  
[[initramfs_internal.h]]  
[[initramfs_test.c]]  
[[version-timestamp.c]]  
[[Kconfig]]  
[[Makefile]]  
[[.gitignore]]  
[[.kunitconfig]]

---

## Ignore for now

Do not worry about:

- compiler attributes
    
- linker sections
    
- boot assembly
    
- build system details
    
- architecture-specific branches
    

Focus on understanding the order of initialization.

---
## Mental model

init/ does not perform one job.

It coordinates the transition from "kernel exists"  
to "kernel can manage the system".

Most files here prepare another subsystem and hand  
control forward.

---
## Contributor angle

Good first contributions:

→ documentation  
→ comments  
→ cleanup  
→ KUnit tests

Avoid changing startup ordering until you understand  
dependency relationships.

---
## Connects to

[[02-Subsystems/mm/_index|mm/]]  
Memory setup.

[[02-Subsystems/kernel/_index|kernel/]]  
Scheduler and process management.

[[02-Subsystems/fs/_index|fs/]]  
Root filesystem startup.

[[04-Execution-Journeys/_index|Execution Journeys]]

---
## Beginner confusion this clears

init/ is not userspace init.

This directory contains kernel initialization code.

PID 1 appears later.

---

→ [[main.c]] — Start here  
→ [[02-Subsystems/_index|Back to Subsystems]]