---
title: 05_Verification_Test
author: Samizo
date: 2026-02-18
tags:
  - OpenLane
  - Verification
  - SmokeTest
  - sky130
  - Reproducibility
---

# 05. Verification Test  
## — Prove That This Environment Is Real —

---

## 1. Purpose of This Chapter

This chapter exists for one reason only:

> **To prove that the environment is actually correct.**

Not fast.  
Not optimized.  
Not pretty.

Just **correct**.

This verification answers three questions:

- Does OpenLane run end-to-end without stopping?
- Is the PDK referenced correctly?
- Is the toolchain internally consistent?

If any of these fail, **do not proceed**.

---

## 2. Preconditions

You must have completed:

- `01_WSL_Docker_Setup.md`
- `02_OpenLane1_Setup.md`
- `03_OpenLane2_Setup.md`
- `04_PDK_Setup.md`

And you must confirm:

- WSL2 is running
- Docker Desktop is running
- Docker WSL Integration is enabled
- PDK is installed under `/usr/local/share/pdk`

If any of these are uncertain, stop here.

---

## 3. Primary Smoke Test (Mandatory)

This is the **single most important command** in the entire repository.

### 3.1 Enter OpenLane1 Directory

```
cd ~/OpenLane
```

---

### 3.2 Run Official Test

```
make test
```

---

### 3.3 Pass Criteria

You pass if and only if:

- The flow does **not** abort
- All stages complete
- The final result prints `PASS`

Anything else is a failure.

> **Warnings are acceptable.  
Errors are not.**

---

## 4. Minimal Design Flow Test (Strongly Recommended)

This test ensures the flow works beyond synthetic tests.

### 4.1 Run a Sample Design

```
cd ~/OpenLane/designs/spm
make run
```

---

### 4.2 Observe Flow Progression

You should see the flow advance through:

- synthesis
- floorplan
- placement
- routing
- finishing

---

### 4.3 Verify GDS Output

```
ls runs/*/results/final/gds
```

A `.gds` file must exist.

If no GDS is produced, the environment is not valid.

---

## 5. Common Failure Modes

### 5.1 PDK Not Found

Symptoms:

- Flow stops early
- Errors mentioning missing cells or tech files

Cause:

- Incorrect `PDK_ROOT`
- PDK placed under `/mnt/c`

Action:

- Fix placement
- **Do not rebuild**
- Re-run test

---

### 5.2 Docker Errors

Symptoms:

- Container fails to start
- Permission or mount errors

Cause:

- Docker Desktop not running
- WSL Integration disabled

Action:

- Fix Docker
- Re-run test

---

### 5.3 Random Mid-Flow Failure

Symptoms:

- Previously working steps now fail

Cause:

- Environment was modified
- Unintentional update occurred

Action:

- **Rollback immediately**
- Do not debug forward

---

## 6. This Is the Trust Boundary

If `make test` passes here:

> **This environment is now a trusted artifact.**

From this point forward:

- You do not “fix” this environment
- You do not “clean it up”
- You do not “update just one thing”

You **freeze** it.

---

## 7. Mandatory Export (Do Not Skip)

Once verification passes, immediately export the environment.

### 7.1 Shutdown WSL

From PowerShell (Administrator):

```
wsl --shutdown
```

---

### 7.2 Export Distribution

```
wsl --export Ubuntu D:\backup\ubuntu_openlane_verified.tar
```

Store this file in:

- An external drive
- A NAS
- At least two locations

This file **is the environment**.

---

## 8. Pass Criteria Summary

You pass this chapter if:

- `make test` passes
- A real design produces GDS
- The environment is exported immediately

Only then may you proceed.

---

## 9. Next Step

Now we prepare for **inevitable hardware or OS failure**.

➡️ **`06_Migration_WSL_Export.md`**

---

## Final Rule

> **If verification passed once,  
it must never be re-earned.  
Rollback instead.**
