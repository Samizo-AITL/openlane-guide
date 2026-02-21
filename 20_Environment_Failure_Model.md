# 20_Environment_Failure_Model.md
**Why OpenLane Environments Break — And How to Stop It**

---

## Purpose of This Chapter

This chapter explains **why OpenLane environments collapse**  
and why most failures are **not tool bugs**.

The goal is simple:

> **Make environment failure a solved problem.**

Once you understand the failure model,
you stop debugging symptoms and start preventing collapse.

---

## The Core Truth

OpenLane does not break randomly.

It breaks when **environment invariants are violated**.

Every failure you have experienced fits into
one of a small number of structural patterns.

---

## Environment vs Design (Critical Distinction)

Before anything else, separate these concepts:

- **Design**  
  RTL, constraints, floorplan, timing targets  
  → Expected to change and fail

- **Environment**  
  Toolchain, PDK, Docker, WSL, versions  
  → Must remain immutable

Most people debug design problems
by accidentally destroying the environment.

This is the root cause.

---

## The Four Environment Invariants

An OpenLane environment is stable **only if all four invariants hold**.

### Invariant 1 — Toolchain Consistency

- OpenLane version
- Docker image
- OpenROAD build
- Magic / Netgen versions

These must form a **known-good set**.

Updating *any one* breaks the set.

---

### Invariant 2 — PDK Identity

The PDK is not “sky130”.

It is:

- A specific commit
- A specific directory layout
- A specific rule interpretation

Two PDKs with the same name
can behave differently and still look “correct”.

PDK mismatch is silent corruption.

---

### Invariant 3 — Filesystem Semantics

WSL has **two filesystems**:

- Native Linux filesystem (safe)
- `/mnt/c` Windows-mounted filesystem (unsafe)

Running OpenLane on `/mnt/c` introduces:

- Non-POSIX behavior
- File locking anomalies
- Performance collapse
- Random tool failures

This is not optional.
This is physics.

---

### Invariant 4 — Temporal Stability

Environments rot over time due to:

- OS updates
- Docker updates
- WSL kernel changes
- Python dependency drift

If you do not **freeze and export**,
time will break your environment for you.

---

## The Standard Failure Patterns

Almost every OpenLane failure maps to one of these patterns.

---

### Pattern 1 — “It Worked Yesterday”

Cause:
- Silent update (Docker, OS, Python)
- Cached images replaced
- Kernel or filesystem behavior changed

Symptom:
- Random new errors
- Same commands, different results

Fix:
- Roll back via WSL import
- Do not investigate further

---

### Pattern 2 — “GLS Is All X”

Cause:
- PDK mismatch
- Missing primitives
- Wrong library order

Symptom:
- Unknown modules
- X-propagation everywhere

Fix:
- Verify PDK identity
- Never patch manually
- Restore environment

---

### Pattern 3 — “STA and GLS Disagree”

Cause:
- Environment inconsistency
- Different libraries used by tools
- Timing data generated under different assumptions

Symptom:
- STA clean, GLS fails (or vice versa)

Fix:
- Align environment
- Regenerate timing artifacts
- Never trust mixed-origin files

---

### Pattern 4 — “I Fixed It and Now Something Else Broke”

Cause:
- Manual fixes inside the environment
- Partial updates
- Ad-hoc patches

Symptom:
- Cascading failures
- Non-reproducible behavior

Fix:
- Stop
- Restore
- Never hot-fix environments

---

## Why Rebuilding Is the Wrong Response

Rebuilding feels productive.
It is not.

Rebuilds:

- Change multiple variables at once
- Destroy forensic information
- Mask the original cause
- Waste time

**Reproducibility beats repair.**

---

## The Correct Recovery Model

When failure occurs:

1. Stop immediately
2. Do not “try one more thing”
3. Export the current state (if possible)
4. Import last known-good image
5. Resume work

This is not laziness.
This is engineering discipline.

---

## Why Export / Import Works

WSL export/import preserves:

- Exact filesystem state
- Tool binaries
- PDK layout
- Dependency graph

It bypasses:

- Install scripts
- Network availability
- Upstream deletions
- Version drift

It turns environment setup
from a process into an artifact.

---

## Environment as an Asset

Treat your OpenLane environment as:

- A compiled binary
- A golden image
- A physical measurement setup

You do not “fix” these.
You **replace them with known-good instances**.

---

## The End State

When done correctly:

- Environment failures disappear
- Debug time collapses
- Focus returns to design and timing
- OpenLane becomes predictable

Not easy.
Predictable.

---

## Chapter Conclusion

OpenLane environments break because:

- Invariants are violated
- Updates are uncontrolled
- Rebuilds destroy causality

They stop breaking when:

- Environments are frozen
- Changes are isolated
- Recovery is instant

---

## Next Chapter

👉 **21_Final_Rules_of_Survival.md**

---
