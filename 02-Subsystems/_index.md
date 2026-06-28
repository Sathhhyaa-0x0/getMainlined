---
title: 02-Subsystems
---
# Subsystems

> "You don't contribute to Linux.  
> You contribute to a subsystem.  
> Pick one. Go deep."

---

## What is a subsystem?

A subsystem is a major area of responsibility  
inside the Linux kernel.

Most subsystems have:

- maintainers
    
- mailing lists
    
- review culture
    
- coding conventions
    
- long-term contributors
    

Learning Linux usually means learning one  
subsystem deeply — not the whole tree.

---

## 🟢 Good Starting Points

Readable. Lower context requirement.  
Good places to learn kernel workflow.

|Subsystem|Why start here|
|---|---|
|[[init/_index\|init/]]|Learn how Linux starts|
|[[Documentation/_index\|Documentation/]]|Best place for first contribution|
|[[samples/_index\|samples/]]|Small example kernel code|
|[[scripts/_index\|scripts/]]|Build and helper tooling|
|[[tools/_index\|tools/]]|Userspace utilities around kernel|

---

## 🟡 Build Core Concepts First

Learn process model, memory, and kernel basics.

|Subsystem|Focus|
|---|---|
|[[kernel/_index\|kernel/]]|Scheduling, timers, signals|
|[[fs/_index\|fs/]]|Filesystems|
|[[ipc/_index\|ipc/]]|Process communication|
|[[security/_index\|security/]]|Security frameworks|
|[[block/_index\|block/]]|Storage layer|
|[[lib/_index\|lib/]]|Shared utilities|
|[[crypto/_index\|crypto/]]|Cryptographic infrastructure|

---

## 🔴 Deep Systems Territory

Subsystem interactions become heavier here.

|Subsystem|Focus|
|---|---|
|[[net/_index\|net/]]|Networking stack|
|[[drivers/_index\|drivers/]]|Hardware support|
|[[sound/_index\|sound/]]|Audio stack|
|[[virt/_index\|virt/]]|Virtualization|
|[[rust/_index\|rust/]]|Rust integration|

---

## ⚫ Internals

These reward patience and repeated reading.

|Subsystem|Focus|
|---|---|
|[[mm/_index\|mm/]]|Memory management|
|[[arch/_index\|arch/]]|Architecture internals|
|[[io_uring/_index\|io_uring/]]|High-performance async I/O|

---

## If you don't know where to begin

Want your first patch?  
→ [[Documentation/_index|Documentation]]

Want to understand startup?  
→ [[init/_index|init]]

Interested in filesystems?  
→ [[fs/_index|fs]]

Interested in hardware?  
→ [[drivers/_index|drivers]]

Interested in networking?  
→ [[net/_index|net]]

Want a broad map first?  
→ [[01-Root-Overview/_index|Root Overview]]

---

## Mental model

Subsystems are not chapters.

They are neighborhoods.

You do not finish one and move on.

You revisit them repeatedly and gradually  
build a map of how they connect.

---

## Next

Pick one subsystem.

Read its index.

Open one file.

Follow one symbol.