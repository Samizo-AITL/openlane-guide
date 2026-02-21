---
title: 03_OpenLane2_Setup
author: Samizo
date: 2026-02-18
tags:
  - OpenLane
  - OpenLane2
  - OpenROAD
  - ASIC
  - Reproducibility
  - Coexistence
---

# 03. OpenLane2 Setup  
## — Isolate It Completely. Never Mix With OpenLane1 —

---

## 1. Purpose of This Chapter (Very Important)

OpenLane2 is the **successor** to OpenLane1.

However, in this guide:

> **OpenLane2 is NOT a replacement.**  
> **It is an evaluation-only environment.**

The goals of this chapter are:

- Keep OpenLane1 **absolutely stable**
- Install OpenLane2 **in complete isolation**
- Prevent accidental cross-contamination
- Allow safe experimentation without risking production flow

If OpenLane1 breaks, **this chapter has failed**.

---

## 2. Key Differences You Must Understand

OpenLane2 differs fundamentally from OpenLane1:

- Python-based CLI (not Makefile-driven)
- Different configuration philosophy
- Faster feature evolution
- Less stability across versions

Because of this:

> **OpenLane2 must never be treated as a production tool (yet).**

---

## 3. Absolute Isolation Rules (Non-Negotiable)

You must enforce **all** of the following:

- Separate directory from OpenLane1
- No shared PATH entries
- No shared aliases
- No shared virtual environments
- No shared PDK manipulation

### Required Directory Layout

```
~/OpenLane     ← OpenLane1 (stable, production)
~/openlane2    ← OpenLane2 (evaluation only)
```

If you violate this, rollback is required.

---

## 4. Clone OpenLane2

### 4.1 Repository Clone

From WSL home:

```
cd ~
git clone https://github.com/efabless/openlane2.git
cd openlane2
```

---

### 4.2 Version Policy

- Use the cloned commit as-is
- Do **not** pull updates automatically
- Treat each commit as disposable

> **Evaluation environments are allowed to break.  
Production environments are not.**

---

## 5. Python Virtual Environment Setup

OpenLane2 requires Python isolation.

### 5.1 Create Virtual Environment

```
cd ~/openlane2
python3 -m venv venv
source venv/bin/activate
```

Your shell prompt should now indicate `(venv)`.

---

### 5.2 Install Dependencies

```
pip install --upgrade pip
pip install -r requirements.txt
```

This may take some time.

---

## 6. Minimal Sanity Check

Do **not** run full flows yet.

### 6.1 CLI Check

```
openlane --help
```

If that fails:

```
python -m openlane --help
```

If help text appears, OpenLane2 is minimally functional.

---

## 7. Verify Non-Interference With OpenLane1

After installing OpenLane2, **immediately verify**:

```
cd ~/OpenLane
make test
```

### Required Result

- Test still passes
- No new errors
- No Docker image changes
- No file changes inside `~/OpenLane`

If this fails:

> **Rollback immediately using WSL import.**

---

## 8. Operational Policy for OpenLane2

Correct usage:

- Feature exploration
- Macro / SRAM experiments
- Future flow evaluation
- Reading logs and behavior

Incorrect usage:

- Production tapeouts
- Benchmarking stability
- Replacing OpenLane1 results
- Copying artifacts into OpenLane1

> **Results from OpenLane2 are disposable.  
OpenLane1 results are assets.**

---

## 9. State at Completion (Pass Criteria)

At the end of this chapter:

- OpenLane1: stable and untouched
- OpenLane2: functional but isolated
- No shared state
- No ambiguity about which tool is used

This is the **only safe coexistence model**.

---

## 10. Next Step

Next, we handle the most valuable asset in the entire system:

➡️ **`04_PDK_Setup.md`**

This is where rebuild cost becomes extremely high.  
Proceed carefully.

---

## Final Reminder

If you ever feel tempted to “merge” OpenLane1 and OpenLane2:

> **Stop. Clone. Isolate. Never mix.**
