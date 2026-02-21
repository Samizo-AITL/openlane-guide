---
title: 04_PDK_Setup
author: Samizo
date: 2026-02-18
tags:
  - OpenLane
  - PDK
  - sky130
  - gf180
  - open_pdks
  - Reproducibility
  - AssetProtection
---

# 04. PDK Setup  
## — The Most Expensive Asset. Build Once. Never Rebuild —

---

## 1. Purpose of This Chapter (Critical)

The Process Design Kit (PDK) is:

- Large in size
- Time-consuming to build
- Extremely sensitive to version mismatches
- Difficult to reproduce exactly
- The **single most valuable asset** in the OpenLane environment

This chapter exists to ensure that:

- sky130 / gf180 PDKs are installed **correctly**
- OpenLane1 and OpenLane2 can **safely reference** them
- The PDK is **built exactly once**
- You will **never rebuild it again**

> **Rebuilding a PDK is a failure, not a maintenance task.**

---

## 2. Absolute Placement Rules (Non-Negotiable)

### Mandatory Rules

- PDKs must live **inside WSL**, never on `/mnt/c`
- PDKs must be stored in **one canonical location**
- All tools must reference the same PDK tree

### Required Location

```
~/pdk
```

If your PDK exists anywhere else, you are creating future failure.

---

## 3. open_pdks Repository

### 3.1 Clone Repository

From WSL home:

```
cd ~
git clone https://github.com/RTimothyEdwards/open_pdks.git
cd open_pdks
```

---

### 3.2 Version Policy

- Use the cloned commit as-is
- Do **not** chase newer commits
- Treat this commit as frozen

> **The first working commit is the correct one.**

---

## 4. System Dependencies

Before building, ensure required packages exist.

```
sudo apt update
sudo apt install -y \
  git make \
  autoconf automake libtool \
  python3 python3-pip \
  tcl-dev tk-dev \
  libcairo2-dev
```

Do not skip this step.

---

## 5. Build sky130 PDK

### 5.1 Configure

```
cd ~/open_pdks
./configure --enable-sky130-pdk
```

---

### 5.2 Build and Install

```
make
sudo make install
```

⚠️ This step takes a long time.  
⚠️ Interrupting it may corrupt the build.

---

### 5.3 Verify Installation

```
ls /usr/local/share/pdk/sky130A
```

You should see directories such as:

- `libs.ref`
- `libs.tech`

If not, **do not proceed**.

---

## 6. Build gf180 PDK (Optional)

If you do not need gf180, skip this section.

### 6.1 Clean Previous Build

```
cd ~/open_pdks
make clean
```

---

### 6.2 Configure and Build

```
./configure --enable-gf180mcu-pdk
make
sudo make install
```

---

### 6.3 Verify

```
ls /usr/local/share/pdk/gf180mcuC
```

---

## 7. Verify Tool Access

### 7.1 OpenLane1

```
cd ~/OpenLane
ls pdks
```

Expected to see symlinks or directories pointing to:

- `sky130A`
- `gf180mcu*` (if built)

---

### 7.2 OpenLane2

```
cd ~/openlane2
ls ~/.volare
```

PDK references should be visible and consistent.

---

## 8. Absolute Prohibitions (Read Carefully)

Never do the following:

- ❌ Re-clone `open_pdks`
- ❌ Rebuild PDK “just to be safe”
- ❌ Keep multiple PDK versions
- ❌ Copy PDKs between directories
- ❌ Place PDKs under `/mnt/c`

> **One PDK. One location. One truth.**

---

## 9. Pass Criteria

You pass this chapter if:

- sky130 PDK is usable
- gf180 (if built) is usable
- OpenLane1 and OpenLane2 both see the same PDK
- You have no intention of rebuilding it

At this point, the **environment’s asset value peaks**.

---

## 10. Next Step

Now we must **prove** that everything works.

➡️ **`05_Verification_Test.md`**

Only after successful verification are you allowed to export the environment.

---

## Final Warning

If you rebuild your PDK later:

> **You ignored this chapter.  
Rollback and start from export.**
