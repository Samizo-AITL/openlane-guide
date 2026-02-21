# APPENDIX: Operational Rules  
## How to Keep Your OpenLane Environment Alive Forever

---

## Purpose of This Document

This appendix defines **non-negotiable operational rules** for using OpenLane.

It does not explain *how OpenLane works*.  
It explains **how not to destroy a working environment**.

If you follow these rules, you will:
- Never lose a working setup
- Never waste days rebuilding environments
- Never panic after updates or failures

---

## The Single Most Important Rule

> **A working OpenLane environment is an asset, not a workspace.**

You do not “fix” assets.  
You **protect** them.

---

## Core Operational Principles

### Rule 1 — Do Not Fix. Roll Back.

If something breaks:
- ❌ Do NOT debug first
- ❌ Do NOT reinstall
- ❌ Do NOT update dependencies

✅ **Rollback via WSL import immediately**

Time spent debugging a broken environment is almost always wasted.

---

### Rule 2 — Do Not Update. Clone.

If you want to try:
- A newer OpenLane version
- A new PDK
- OpenLane2 features
- Experimental flows

✅ **Clone or import a separate environment**

Never update the working one.

---

### Rule 3 — Do Not Rebuild. Export & Import.

Rebuilding environments is:
- Slow
- Error-prone
- Non-reproducible

Exporting and importing is:
- Fast
- Exact
- Guaranteed

If rebuild seems easier, you are already making a mistake.

---

## Daily Usage Rules (DO / DON’T)

### ✅ DO

- Work only inside WSL home (`~`)
- Treat `~/OpenLane` and PDK directories as read-only assets
- Export WSL after:
  - PDK changes
  - Verified successful runs
  - Major milestones
- Keep at least **two generations** of exports

---

### ❌ DON’T

- Do NOT run OpenLane under `/mnt/c`
- Do NOT mix OpenLane1 and OpenLane2 files
- Do NOT run `git pull` on a working environment
- Do NOT rebuild PDKs “just to be safe”
- Do NOT debug before exporting the current state

---

## OpenLane1 vs OpenLane2 Operational Separation

### OpenLane1 (Primary / Stable)

- Used for real designs
- Makefile-based
- Docker-centered
- Treated as **production environment**

Rules:
- No updates
- No experiments
- No mixing with OpenLane2

---

### OpenLane2 (Secondary / Evaluation)

- Used only for testing new ideas
- Python-based
- Actively changing

Rules:
- Must live in a separate directory
- Must never modify OpenLane1 outputs
- Results must not be copied blindly

---

## PDK Handling Rules

PDKs are the **highest-value assets**.

### Mandatory Rules

- Single source of truth
- Single version per environment
- Never rebuild unless absolutely required
- Never mix versions

If LVS/DRC results change unexpectedly:
→ **Assume PDK mismatch first**

---

## When Something Goes Wrong: Decision Table

| Symptom | Correct Action |
|------|----------------|
| Flow fails after update | Import previous WSL |
| GLS shows unknown modules | Check PDK, then rollback |
| All-X waveforms | Rollback before debugging |
| Docker behaves strangely | Rollback |
| Cause unclear | Rollback |

If rollback fixes it, you are done.

---

## Export Timing Rules

You must export WSL:

- After confirming `make test` passes
- After PDK installation or change
- Before attempting any “fix”
- Before experimenting

Recommended command:

```powershell
wsl --shutdown
wsl --export Ubuntu D:\backup\ubuntu_openlane_verified.tar
```

This file **is your environment**.

---

## Mental Model to Adopt

Stop thinking like this:
> “I’ll just try to fix it.”

Start thinking like this:
> “This environment already works. I will not risk it.”

This mindset alone prevents 90% of OpenLane disasters.

---

## Final Statement

If you remember nothing else, remember this:

> **Broken environments are optional.  
> Only unprotected environments break.**

This repository exists so you never learn that lesson the hard way again.

---
