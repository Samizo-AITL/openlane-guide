---
title: 02_OpenLane1_Setup
author: Samizo
date: 2026-02-18
tags:
  - OpenLane
  - OpenLane1
  - OpenROAD
  - sky130
  - gf180
  - ASIC
  - Reproducibility
---

# 02. OpenLane1 Setup  
## — Freeze a Known-Good Production Flow —

---

## 1. Position of This Chapter (Critical)

This chapter is **not** about installing the “latest” OpenLane.

The sole purpose is:

- Install OpenLane1 **once**
- Confirm it works
- **Freeze the entire environment**
- Never update it in-place again

In this guide:

> **A working OpenLane1 environment is a frozen asset, not a moving target.**

---

## 2. Preconditions

You must have completed:

- `01_WSL_Docker_Setup.md`
- WSL2 enabled
- Docker Desktop working with WSL
- `docker run hello-world` succeeds

If any of these are uncertain, **stop and fix them first**.

---

## 3. Directory Policy (Non-Negotiable)

### Required Rule

All work must be done **inside WSL home**.

Recommended location:

```
~/OpenLane
```

### Forbidden

- `/mnt/c`
- Windows filesystem paths
- Shared folders

Violating this rule causes I/O instability and Docker issues.

---

## 4. Clone OpenLane1

### 4.1 Clone Repository

Inside WSL:

```
cd ~
git clone https://github.com/The-OpenROAD-Project/OpenLane.git
cd OpenLane
```

This repository currently contains **OpenLane1 (Makefile-based flow)**.

---

### 4.2 Version Policy

- Use the cloned state **as-is**
- Do **not** switch branches
- Do **not** pull updates

> **The commit that works is the correct version.**

---

## 5. Initial OpenLane1 Setup

### 5.1 Pull Docker Image

Run:

```
make pull-openlane
```

This step:

- Pulls the official OpenLane Docker image
- Prepares the toolchain

This may take several minutes.

---

### 5.2 Verify Docker Image

```
docker images | grep openlane
```

If an OpenLane image appears, this step is complete.

---

## 6. PDK Status (Do Not Build Yet)

At this stage:

- **Do not** build PDK
- **Do not** modify PDK
- **Do not** troubleshoot PDK errors

Just verify the directory exists:

```
ls pdks
```

Actual PDK setup is handled **later** in `04_PDK_Setup.md`.

---

## 7. Smoke Test (Mandatory)

### 7.1 Run Official Test

From the OpenLane directory:

```
make test
```

---

### 7.2 Expected Result

A successful run:

- Does not abort
- Completes the flow
- Ends with a `PASS` message

This moment defines the **golden environment state**.

---

## 8. What You Must NOT Do After This

Once `make test` passes:

❌ `git pull`  
❌ Docker image updates  
❌ Re-clone OpenLane  
❌ PDK rebuild attempts  

These actions **destroy reproducibility**.

---

## 9. Asset Mindset

From this point forward:

- OpenLane1
- Docker image
- Directory layout

are a **single inseparable asset**.

> Treat this environment like firmware, not software.

---

## 10. Next Step

Next, we address OpenLane2 —  
**without contaminating this stable OpenLane1 setup**.

➡️ **Next: `03_OpenLane2_Setup.md`**

---

## Note on Export Timing

Do **not** export WSL yet.

Reasons:

- PDK is not finalized
- Asset value is incomplete

Export is done **after verification**, not now.
