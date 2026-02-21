# openlane-guide

> **Read this repository and stop breaking your OpenLane environment forever.**

This repository is a **battle-tested, failure-driven guide** for running OpenLane  
in a **stable, reproducible, and disaster-proof way**.

It is not a feature list.  
It is not a quick-start blog post.

This guide exists for one reason only:

> **So you never waste time rebuilding a broken OpenLane environment again.**

---

## What this guide is

This repository documents **what actually works** after real-world failures involving:

- WSL2 + Docker instability
- PDK version mismatches
- OpenLane1 vs OpenLane2 confusion
- GLS failures (unknown modules, all-X waveforms)
- STA / OpenROAD dead ends
- Environment corruption after updates
- Irrecoverable Classic OpenLane setups

Everything here is written from one perspective only:

> **“How do I make sure this never breaks again?”**

This is not theoretical advice.  
Every rule here exists because something *already failed*.

---

## What this guide is NOT

- ❌ Verilog language tutorial  
- ❌ ASIC theory textbook  
- ❌ OpenLane option reference  
- ❌ “Latest version” chasing guide  

If you want syntax or theory, plenty of resources already exist.

This guide focuses on **operational survival**.

---

## Who this guide is for

This guide is for:

- Engineers who already tried OpenLane and got burned
- People who want **reproducibility**, not novelty
- Anyone who values **environment stability over updates**
- Those who want to understand *why* things break, not just *how* to run commands

If you have never broken OpenLane before:  
you probably will — unless you read this first.

---

## How to read this repository (IMPORTANT)

This is **not a reference manual**.  
**Order matters.**

Recommended reading order:

1. `01_WSL_Docker_Setup.md`  
2. `02_OpenLane1_Setup.md`  
3. `03_OpenLane2_Setup.md`  
4. `04_PDK_Setup.md`  
5. `05_Verification_Test.md`  
6. `06_Migration_WSL_Export.md`  
7. `07_Troubleshooting.md`

Skipping steps defeats the entire purpose of this guide.

---

## Core philosophy

This repository is built on a few non-negotiable rules:

- **Do not fix. Roll back.**
- **Do not update. Clone.**
- **Do not rebuild. Export & import.**
- **Your environment is an asset, not a workspace.**

Once you adopt this mindset, OpenLane stops being “difficult”.

---

## Supported scope

This guide explicitly covers:

- OpenLane1 (Makefile-based, stable, production-oriented)
- OpenLane2 (evaluation-only, fully isolated)
- sky130 / gf180 PDK
- WSL2 + Docker Desktop
- GLS (Icarus Verilog)
- OpenROAD / OpenSTA
- Magic / KLayout
- Disaster recovery via WSL export/import

Anything outside this scope is intentionally excluded.

---

## Repository guarantee

If you follow this repository **in order**, you will get:

- A working OpenLane environment
- A reproducible setup you can migrate in minutes
- A flow that survives OS, Docker, and hardware failures

If something breaks, the problem is **not** OpenLane.

It is deviation from this guide.

---

## Final note

If this repository saves you **even one full reinstall**,  
it has already done its job.

---

**Environment failures are optional.  
This guide shows you how.**
