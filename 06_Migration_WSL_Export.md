---
title: 06_Migration_WSL_Export
author: Samizo
date: 2026-02-18
tags:
  - OpenLane
  - WSL2
  - Migration
  - Backup
  - DisasterRecovery
  - Reproducibility
---

# 06. WSL Environment Migration (Export / Import)  
## — Recover in 15 Minutes Even If the PC Dies —

---

## 1. Purpose of This Chapter (Critical)

This chapter defines the **only correct way** to protect your OpenLane environment.

It assumes the following failures **will happen**:

- Laptop motherboard failure
- SSD corruption
- Windows boot failure
- Forced OS reinstall
- Docker Desktop breakage
- Accidental environment destruction

This chapter turns all of the above into **non-events**.

> **You do not rebuild environments.  
You move them.**

---

## 2. Core Migration Philosophy

### ✔ Correct Approach

- Export the entire WSL distribution as a `.tar`
- Import it verbatim on another machine
- Perform **zero** Linux-side reconstruction

### ✖ Incorrect Approach

- Reinstall Ubuntu
- Re-clone OpenLane
- Rebuild PDKs
- “Try to remember what worked”

That is **re-development**, not recovery.

---

## 3. Export Procedure (Source Machine)

### 3.1 Identify WSL Distribution Name

From PowerShell (Administrator):

```
wsl -l -v
```

Example:

```
NAME      STATE   VERSION
Ubuntu    Running 2
```

Record the exact name.

---

### 3.2 Fully Stop WSL

```
wsl --shutdown
```

This is mandatory.  
Exporting a running distribution is unsafe.

---

### 3.3 Perform Export (Most Important Step)

```
wsl --export Ubuntu D:\backup\ubuntu_openlane_verified.tar
```

### Storage Rules

- Never store only on the internal SSD
- Use external SSD / NAS / cloud
- Keep **at least two copies**

> **This tar file *is* your environment.**

---

## 4. Import Procedure (Target Machine)

### 4.1 Prerequisites

On the new machine:

- Windows 11 installed
- BIOS virtualization enabled
- WSL2 enabled (`wsl --install`)
- Docker Desktop installed

Do **not** install Ubuntu manually.

---

### 4.2 Create Import Directory

Example:

```
mkdir C:\WSL\Ubuntu-OpenLane
```

This directory must be empty.

---

### 4.3 Import Distribution

```
wsl --import Ubuntu-OpenLane C:\WSL\Ubuntu-OpenLane D:\backup\ubuntu_openlane_verified.tar --version 2
```

---

### 4.4 Launch Imported Environment

```
wsl -d Ubuntu-OpenLane
```

Inside WSL:

```
ls
```

You must see:

- OpenLane
- openlane2
- pdk / open_pdks
- design directories

If anything is missing, stop.

---

## 5. Docker Re-Integration (Mandatory)

### 5.1 Docker Desktop Settings

Open Docker Desktop:

- Settings → Resources → WSL Integration
- Enable integration for **Ubuntu-OpenLane**

This step is required every time you import.

---

### 5.2 Verify Docker Works

Inside WSL:

```
docker run --rm hello-world
```

If this fails, Docker is not integrated correctly.

---

## 6. OpenLane Validation After Import

### 6.1 Minimal Confirmation

```
cd ~/OpenLane
make test
```

If this passes, recovery is complete.

No further validation is required.

---

## 7. Common Migration Failures

### ❌ Installed Ubuntu Before Import

Result:
- Import overwrites or conflicts

Corrective Action:
- Delete distribution
- Re-import cleanly

---

### ❌ Docker Does Not Work

Cause:
- WSL Integration disabled

Action:
- Fix Docker settings
- Retry

---

### ❌ PDK Missing

Cause:
- PDK was stored under `/mnt/c`

Action:
- This environment is invalid
- Roll back to a correct export

---

## 8. Operational Rules (Non-Negotiable)

- Export after any confirmed-good change
- Keep multiple generations
- Never trust a single copy
- Prefer rollback over repair

---

## 9. Real-World Value

Using this method:

- Environment rebuild time: **0 minutes**
- Mental cost: **near zero**
- Hardware failure impact: **none**

> **Your work continues as if nothing happened.**

---

## 10. Next Step

The final chapter defines how environments are destroyed — and how to avoid it.

➡️ **`07_Troubleshooting.md`**

---

## Final Statement

> **An OpenLane environment is not a setup.  
It is a deliverable.  
Treat it accordingly.**
