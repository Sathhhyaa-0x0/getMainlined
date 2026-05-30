# Welcome to getMainlined

> "Your path from zero to first kernel patch."

---

## What is this?

getMainlined is a navigation and orientation guide for anyone who wants to contribute to the Linux kernel but doesn't know where to start.

---

## What this is NOT

This is not yet another "how the kernel works" resource. Plenty of those exist already:

- linux-insides → deep concept explanations
- makelinux kernel map → visual architecture
- hackerbikepacker.com → contributor workflow
- lewboski.dev → real first contribution story

Read those too. They're excellent.

---

## What getMainlined is

When you open torvalds/linux on GitHub and see 70,000 files — this is your map.

getMainlined answers what others don't:

- What does each folder actually do?
- How do subsystems connect to each other?
- Where should I look to make my first patch?
- What should I read first as a contributor?

---

## Who this is for

→ Developers who want to contribute to Linux
→ CS students studying OS internals
→ Embedded/driver developers starting out
→ Anyone who opened the repo and felt lost

---

## Who this is NOT for

→ Someone who just wants to use Linux
→ Someone looking for sysadmin guides
→ Someone wanting /bin /etc /home explained

---

## What's inside this vault

[[00-START-HERE/_index|START HERE]]
You are here. Read this first. Glossary, recommended paths, how to navigate.

[[01-Root-Overview/_index|Root Overview]]
Your first stop after this. Every folder in torvalds/linux explained. What each subsystem is in plain English.

[[02-Subsystems/_index|Subsystems]]
Deep dive into each major folder. What it does, why it exists, key files, difficulty rating, contributor angle.

[[03-Key-Files/_index|Key Files]]
~50 landmark files across the entire kernel. The files that make beginners go "ohh THAT'S how it works."

[[04-Execution-Journeys/_index|Execution Journeys]]
Trace one action across multiple subsystems. What happens when you open a file? How does fork() work end to end? The big picture connections.

[[05-Contributor-Paths/_index|Contributor Paths]]
Ready to contribute? Pick your subsystem and follow the path. Includes your first patch guide.

[[06-Concepts/_index|Concepts]]
Supporting knowledge. Syscalls, modules, memory, processes. Read these when a subsystem note mentions something unfamiliar.

[[07-Meta/_index|Meta]]
About this project. How to contribute to getmainlined itself. Changelog.

---

## Where to start

First time here? Follow this exact order:

1. Finish reading this note ← you are here
2. [[01-Root-Overview/_index|Root Overview]] ← go here next
3. Pick one subsystem from [[02-Subsystems/_index|Subsystems]] that interests you
4. When ready → [[05-Contributor-Paths/_index|Your First Patch]]

Don't try to read everything. Navigate to what you need. That's the whole point.

---

## Difficulty System

Every note is rated:

🟢 Beginner — no prerequisites
🟡 Intermediate — some kernel concepts needed
🔴 Advanced — serious study needed
⚫ Wizard Territory — years of experience

---

## The Goal

You open getmainlined confused. You close it knowing exactly where to go and what to do next.

That's it. That's the whole mission.