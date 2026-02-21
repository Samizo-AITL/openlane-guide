---
title: 07_Troubleshooting
author: Samizo
date: 2026-02-18
tags:
  - OpenLane
  - Troubleshooting
  - FailurePrevention
  - DisasterAvoidance
  - Reproducibility
---

# 07. Troubleshooting  
## — The Final Checklist for Never Breaking Your Environment —

---

## 1. Role of This Chapter

This chapter is **not** a guide for fixing errors.

It exists for one purpose only:

> **To prevent you from destroying a working OpenLane environment.**

If you are reading this *after* something broke,  
you are already late — but you can still avoid making it worse.

---

## 2. The Three Non-Negotiable Rules

Memorize these rules.  
Everything else is secondary.

### Rule 1  
**If it works, do not touch it.**

### Rule 2  
**If you want to change something, clone the environment first.**

### Rule 3  
**If something breaks, roll back. Do not repair.**

Violating any of these rules guarantees failure.

---

## 3. Common Environment Destruction Patterns

These are not theoretical.  
They are documented real failures.

---

### ❌ Running `git pull`

**Symptoms**
- Yesterday’s working flow fails
- Configuration behavior silently changes

**Reality**
- You changed the environment contract

**Correct Action**
- Stop immediately
- Import the last known-good WSL export
- Continue working

---

### ❌ Rebuilding or Reinstalling the PDK

**Symptoms**
- DRC/LVS results change
- Magic or Netgen behavior differs
- GLS fails unexpectedly

**Reality**
- You invalidated the design basis

**Correct Action**
- Roll back to the previous export
- Never rebuild a working PDK

---

### ❌ Working Under `/mnt/c`

**Symptoms**
- Severe I/O slowdown
- Docker instability
- Random permission errors

**Reality**
- You violated WSL’s performance model

**Correct Action**
- Move everything under WSL home
- Export → import to sanitize the environment

---

### ❌ Docker Desktop Update Breaks Everything

**Symptoms**
- Containers fail to start
- Permission or mount errors

**Reality**
- Docker is external and unversioned

**Correct Action**
- Check WSL integration settings
- If unresolved, import a clean environment

---

## 4. What To Do the Moment Something Feels Wrong

Do **not** investigate first.

Do this **immediately**:

```powershell
wsl --shutdown
wsl --export Ubuntu D:\backup\ubuntu_openlane_before_fix.tar
```

Only after exporting are you allowed to think.

> **Debugging without a snapshot is reckless.**

---

## 5. Correct Way to Experiment or Update

### The Only Safe Pattern

```
Stable Environment
        ↓ clone
Test / Experiment Environment
```

Example:

```powershell
wsl --import Ubuntu-OpenLane-Test C:\WSL\Test D:\backup\ubuntu_openlane_verified.tar
```

Destroy the test environment freely.  
The stable one remains untouched.

---

## 6. Decision Table (Use This, Not Instinct)

| Situation | Action |
|---------|--------|
| Flow error | Import |
| PDK mismatch | Import |
| Docker failure | Import |
| OS update issue | Import |
| Unknown cause | Import |

If you hesitate, you already know the answer.

---

## 7. Backup Discipline (Recommended)

- Export after:
  - Successful environment verification
  - PDK completion
  - Major configuration milestones
- Keep at least two generations
- Store backups on different physical media

---

## 8. Final Conclusions

- Do not nurture environments
- Freeze them
- Move them intact
- Replace repair with rollback

Once this mindset is adopted,  
OpenLane stops being fragile.

---

## 9. Repository-Level Summary

This entire repository exists for one goal:

> **To let you focus on design, not environment recovery.**

If you follow chapters 01–07 exactly:

- OpenLane runs end-to-end
- GLS works reliably
- STA and OpenROAD remain usable
- Hardware failures become irrelevant

---

## Final Statement

> **Only engineers who can protect their environment  
are able to move designs forward.**

This guide is written for your future self.  
Treat it as an insurance policy.
