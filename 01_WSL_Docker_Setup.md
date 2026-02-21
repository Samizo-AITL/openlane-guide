---
title: 01_WSL_Docker_Setup
author: Samizo
date: 2026-02-18
tags:
  - OpenLane
  - WSL2
  - Docker
  - Windows11
  - EnvironmentSetup
  - Reproducibility
---

# 01. WSL2 / Docker Setup  
## — Build an OpenLane Foundation That Never Breaks —

---

## 1. Purpose of This Chapter (Critical)

The purpose of this chapter is **not** to “install Linux”.

The real goals are:

- Run OpenLane **stably**
- Ensure **WSL export / import always works**
- Survive PC failure, OS reinstall, or disk replacement **without rebuilding**

In short:

> **Create a WSL2 environment that is reproducible, portable, and failure-resistant.**

This foundation determines whether OpenLane remains usable long-term.

---

## 2. Prerequisites

You must have:

- Windows 11 (Pro or Home)
- Administrator privileges
- BIOS / UEFI virtualization enabled (VT-x / SVM)

For Lenovo systems, confirm in BIOS:

```
Virtualization Technology = Enabled
```

If virtualization is disabled, **stop here**.

---

## 3. Enable WSL2

### 3.1 Install WSL

Open **PowerShell as Administrator** and run:

```
wsl --install
wsl --set-default-version 2
```

⚠️ **Do NOT install Ubuntu yet.**  
This guide relies on importing a verified environment later.

---

### 3.2 Mandatory Reboot

After enabling WSL:

> **Reboot Windows immediately.**

Skipping this step causes subtle Docker and filesystem failures.

---

## 4. Verify WSL State

After reboot, open PowerShell and run:

```
wsl -l -v
```

Expected output:

```
NAME      STATE    VERSION
Ubuntu    Stopped  2
```

If `VERSION` is not `2`, fix this before proceeding.

---

## 5. Install Docker Desktop

### 5.1 Docker Desktop Installation

- Download Docker Desktop for Windows from the official site
- During installation, ensure:
  - Use WSL 2 based engine is enabled

---

### 5.2 Mandatory Docker Configuration

Open Docker Desktop and verify:

#### Settings → General
- Use the WSL 2 based engine

#### Settings → Resources → WSL Integration
- Enable integration with my default WSL distro
- Enable the target distribution (to be imported later)

If WSL integration is disabled, **OpenLane will not run**.

---

## 6. Verify Docker Operation

From PowerShell or WSL:

```
docker --version
docker run --rm hello-world
```

Successful output:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

If this fails, **do not continue**.

---

## 7. Non-Negotiable WSL Rules

Breaking any rule below **guarantees failure**.

### Required Rules

- OpenLane and PDK **must live inside WSL home (`~`)**
- Docker is used **only via WSL**
- WSL filesystem is authoritative

---

### Forbidden Actions

- VirtualBox or VMware
- WSL1
- Running OpenLane under `/mnt/c`
- Windows-native Docker mode

These destroy reproducibility and performance.

---

## 8. Completion Criteria

You may proceed only if:

- WSL2 is enabled
- Docker Desktop is integrated with WSL
- `docker run hello-world` succeeds

This state is the **bedrock** of a reliable OpenLane environment.

---

## 9. Next Step

Next, we install **OpenLane1** — not to chase updates,  
but to **freeze a known-good configuration**.

➡️ **Next: `02_OpenLane1_Setup.md`**
