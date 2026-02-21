# APPENDIX — OpenLane1 vs OpenLane2: Why Separation Is Mandatory

This appendix explains **why OpenLane1 and OpenLane2 must never be mixed**,  
and how accidental coexistence silently destroys reproducibility.

This is not a preference issue.  
It is a **structural incompatibility problem**.

---

## Executive summary

- OpenLane1 and OpenLane2 are **not different versions of the same tool**
- They are **different systems with different assumptions**
- Mixing them causes:
  - Non-reproducible behavior
  - Configuration overrides
  - PDK binding corruption
  - Silent flow changes

> **If you mix them, you lose control of your environment.**

---

## What OpenLane1 actually is

OpenLane1 is:

- Makefile-driven
- Docker-centered
- Path-implicit
- Convention-based
- Designed for **fixed, stable flows**

Key properties:

- Flow behavior is mostly static
- Configuration files are respected verbatim
- PDK expectations are rigid
- Toolchain versions are frozen by Docker image

This makes OpenLane1 ideal for:
- Production-style flows
- Education
- Long-term reproducibility
- Disaster recovery

---

## What OpenLane2 actually is

OpenLane2 is:

- Python-based
- CLI-driven
- Actively evolving
- Explicitly versioned
- Designed for **experimentation and extensibility**

Key properties:

- Flow logic changes frequently
- Defaults evolve
- Configuration schema is enforced
- PDK handling is abstracted (volare)

This makes OpenLane2 ideal for:
- Research
- New features
- Macro-heavy designs
- Future-oriented evaluation

---

## The illusion of “upgrade”

A common misconception:

> “OpenLane2 is just OpenLane1, but newer.”

This is false.

OpenLane2 does **not** preserve:
- Configuration semantics
- Directory structure assumptions
- Flow ordering
- Failure modes

Treating OpenLane2 as an “upgrade” leads directly to environment corruption.

---

## How mixing actually happens

### Pattern 1: Shared directories

```text
~/OpenLane/
~/OpenLane/openlane2/
```

This causes:
- Accidental PATH resolution
- Shared Python environments
- Tool confusion

---

### Pattern 2: Shared PDK managers

Using:
- open_pdks
- volare
- manual copies

in the same environment causes:
- Competing PDK ownership
- Implicit overrides

---

### Pattern 3: “Just testing something quickly”

The most dangerous pattern.

- Running one OpenLane2 command
- Inside an OpenLane1-prepared environment
- With shared variables

This is how stable systems die.

---

## Observable failure symptoms

When OpenLane1 and OpenLane2 interfere, you may see:

- Flow options silently ignored
- Different results with identical inputs
- PDK path changes without warning
- OpenROAD behavior changes
- Inconsistent STA results
- “It worked yesterday” syndrome

None of these are random.

---

## The correct coexistence model

### Mandatory separation

```text
~/OpenLane        ← OpenLane1 (production)
~/openlane2       ← OpenLane2 (evaluation)
```

Rules:

- No shared virtualenvs
- No shared scripts
- No shared configs
- No shared assumptions

---

## Operational policy (recommended)

- **Design work** → OpenLane1
- **Evaluation work** → OpenLane2
- **Never migrate results backward**
- **Never “try” OpenLane2 inside OpenLane1**

If OpenLane2 proves something valuable:
reimplement it cleanly in OpenLane1.

---

## Why separation increases confidence

By separating:

- You know exactly which system produced which result
- Failures are attributable
- Rollback is trivial
- Reproducibility is preserved

This is not conservatism.
It is engineering discipline.

---

## Final rule

> **OpenLane1 and OpenLane2 may coexist on the same machine.  
> They must never coexist in the same mental model.**

If you remember only one thing:

**Separation is not optional. It is required.**

---
