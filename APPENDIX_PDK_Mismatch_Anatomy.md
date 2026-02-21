# APPENDIX — Anatomy of PDK Mismatches (sky130 / gf180)

This appendix explains **why PDK mismatches are the single most destructive
failure mode** in OpenLane-based flows.

PDK mismatches do not usually fail loudly.
They fail *silently*, *inconsistently*, and *waste enormous amounts of time*.

This document exists so you can **identify, avoid, and permanently eliminate**
this class of failure.

---

## What “PDK mismatch” actually means

A PDK mismatch does **not** mean:

- “The PDK is missing”
- “The PDK build failed”

It means:

> **Different tools are unknowingly using different PDK contents or versions.**

This can happen even when:
- Paths look correct
- Environment variables are set
- Files exist on disk

---

## Why PDK mismatches are so dangerous

PDK mismatches cause failures that appear as:

- LVS mismatches with no obvious cause
- STA results that change between runs
- GLS failures with correct netlists
- DRC violations that “should not exist”
- Behavior that differs across machines

These are **not random bugs**.  
They are deterministic consequences of inconsistency.

---

## The three PDK identity layers

A PDK has **three independent identities**:

### 1. File-system identity
- Directory path
- Symbolic links
- Case sensitivity
- `/mnt/c` vs WSL native filesystem

### 2. Content identity
- Commit hash
- Rule decks
- Standard cell definitions
- UDP primitives
- Tech LEF / routing rules

### 3. Tool binding identity
- Which PDK each tool actually loads
- Magic vs OpenROAD vs Netgen vs Icarus
- Docker container vs host filesystem

A mismatch in *any* of these layers breaks consistency.

---

## Common PDK mismatch patterns

### Pattern 1: Windows / WSL split-brain

#### Symptom
- GDS generated successfully
- GLS fails with unknown modules
- LVS mismatches inexplicably

#### Root cause
- PDK exists in `C:\...`
- Tools are executed inside WSL
- Different filesystem views

#### Rule
> **Never place PDKs under `/mnt/c`. Ever.**

---

### Pattern 2: Partial PDK copy

#### Symptom
- Some cells resolve
- Others fail
- UDP-related errors appear

#### Root cause
- PDK directory copied manually
- `libs.ref` present
- `primitives/` missing or incomplete

#### Rule
> **A partially copied PDK is worse than no PDK.**

---

### Pattern 3: Mixed PDK generations

#### Symptom
- STA results change after “harmless updates”
- LVS passes on one system, fails on another

#### Root cause
- Different sky130 commits
- open_pdks rebuilt at different times
- Unpinned PDK sources

#### Rule
> **“Latest” is not a version. It is a liability.**

---

### Pattern 4: Docker vs host PDK mismatch

#### Symptom
- OpenLane flow succeeds
- Manual GLS fails
- Magic behaves differently inside/outside container

#### Root cause
- Docker sees `/usr/local/share/pdk`
- Host tools see `~/pdk`
- Same name, different contents

#### Rule
> **Docker and host must see the same PDK, or be fully isolated.**

---

## The only safe PDK strategy

### Golden rules

1. **One PDK location**
2. **One PDK version**
3. **One ownership model**
4. **No rebuilds**
5. **No partial copies**

Recommended:

```text
~/pdk/
 ├── sky130A/
 └── gf180mcuC/
```

And nowhere else.

---

## Why rebuilding PDKs is almost always wrong

Rebuilding a PDK:

- Changes rule interpretations
- Changes parasitics
- Changes LVS matching behavior
- Breaks reproducibility

Unless you are *developing the PDK itself*:

> **Rebuilding is regression, not progress.**

---

## Detection checklist

If something feels “off”, check:

- Does every tool point to the same PDK path?
- Is the PDK inside WSL native filesystem?
- Are there multiple sky130 directories?
- Did anything auto-update?
- Was open_pdks rebuilt?

If the answer is “maybe”:
assume **PDK mismatch until proven otherwise**.

---

## The export/import advantage

WSL export/import works because:

- Filesystem state is frozen
- PDK contents are identical
- Paths remain consistent
- Tool bindings do not drift

This is why **export/import is not a backup**.

It is **version control for environments**.

---

## Final principle

> **PDKs are not dependencies.  
> They are assets.**

Treat them accordingly, and OpenLane becomes stable.

Ignore this, and no amount of debugging will save you.

---
