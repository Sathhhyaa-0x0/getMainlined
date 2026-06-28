---
title: main.c
---
# main.c

🟢 Beginner Friendly — but deeply important

Part of [[_index|init/]]

---
## What is this file?

main.c contains the generic startup path of  
the Linux kernel.

Execution begins earlier in architecture-  
specific startup code, but eventually control  
reaches start_kernel() — which lives here.

This file coordinates the transition from:

kernel loaded  
→ kernel initializing  
→ kernel running

Many core subsystems begin their initialization  
sequence from this file.

If you want one place that reveals how Linux  
wakes up — this is it.

---
## Execution Flow

Firmware  
↓  
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
/sbin/init  
↓  
Userspace

This file sits at the center of that transition.

---
## Why it matters

This is one of the most valuable files a beginner  
can read.

Not because it contains the hardest code.

Because it reveals the structure of Linux.

Reading start_kernel() from top to bottom shows:

- which subsystems exist
    
- roughly when they initialize
    
- what depends on what
    
- where to go next
    

It is almost an index of the entire kernel  
hidden inside a function.

---
## Ignore for now

Do not get stuck on:

- compiler attributes
    
- visibility modifiers
    
- sanitizer annotations
    
- stack protection macros
    
- architecture-specific details
    

Focus on:

function names  
call order  
subsystem boundaries

---
## Key function — start_kernel()

```c
asmlinkage __visible __init
__no_sanitize_address
__noreturn
__no_stack_protector

void start_kernel(void)
```

Some attributes worth knowing:

__init  
→ boot-only code section; memory can later be reused

__noreturn  
→ execution never returns to the caller

The others exist mostly to control compiler,  
linker, and instrumentation behavior.

Do not worry about them yet.

Inside, startup happens step by step:

```c
setup_arch(&command_line);

mm_core_init_early();

sched_init();

vfs_caches_init();

rest_init();
```

Each call hands temporary control to another  
subsystem.

Follow any one of them and you leave init/  
and begin exploring a different part of Linux.

---
## The order is not random

Early startup follows dependency order.

Example:

```c
boot_cpu_init();

page_address_init();

setup_arch(&command_line);

mm_core_init_early();
```

Architecture setup happens before memory.

Memory must exist before scheduling.

Scheduling must exist before processes.

Initialization here is not sequential because  
it looks nice — it is sequential because later  
systems depend on earlier ones.

---
## rest_init() — the handoff

Near the end of startup comes:

```c
static noinline void __ref
__noreturn rest_init(void)
```

This function marks a transition.

Until this point:

the kernel is building itself.

After this point:

the kernel begins managing execution.

Inside rest_init(), the kernel creates the task  
that eventually becomes PID 1.

That task later reaches kernel_init().

A small comment nearby explains an important  
ordering constraint:

init must receive PID 1 before worker threads  
begin appearing.

Startup ordering in Linux is intentional.

---
## kernel_init — what actually reaches userspace

A detail many beginners miss:

start_kernel() never directly launches  
userspace.

Instead:

start_kernel()  
→ rest_init()  
→ kernel_init()

kernel_init() eventually tries known init paths:

```c
/sbin/init
/etc/init
/bin/init
/bin/sh
```

If none succeed:

the kernel panics.

That infamous:

"No working init found"

message comes from this path.

---
## How to read this file

Do not try to understand every line.

First pass:

Read only function names.

Build a map.

Second pass:

Pick one function.

Follow it.

Read until confused.

Return.

Repeat.

Kernel reading is exploration —  
not linear study.

---
## Mental model

start_kernel() does not perform kernel work.

It coordinates startup.

Each function temporarily hands control to  
another subsystem, waits for preparation to  
finish, and moves forward.

Reading this file is less about understanding  
boot and more about discovering who exists  
inside Linux.

---
## Contributor angle

Good first contribution?

Carefully yes.

This file receives heavy review because startup  
logic affects the entire kernel.

Good contribution types:

→ documentation  
→ comments  
→ cleanup

Avoid changing initialization ordering until  
you understand subsystem dependencies.

---
## Connects to

[[02-Subsystems/mm/_index|mm/]]  
Memory initialization.

[[02-Subsystems/kernel/_index|kernel/]]  
Scheduler startup.

[[02-Subsystems/fs/_index|fs/]]  
Filesystem initialization.

[[init_task.c]]  
Early task structures.

[[calibrate.c]]  
Boot-time CPU calibration.

[[04-Execution-Journeys/_index|Boot Journey]]

---
## Beginner confusion this clears

The kernel does not suddenly "start."

Linux becomes operational through a deliberate  
sequence of initialization steps.

Subsystems prepare other subsystems.

Order matters.

That order becomes visible here.

---
If this felt manageable:

→ [[init_task.c]]  
→ sched_init()  
→ mm_core_init_early()

If this felt overwhelming:

→ [[04-Execution-Journeys/_index|Boot Journey]]

→ [[_index|Back to init/]]