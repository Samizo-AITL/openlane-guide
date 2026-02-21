# APPENDIX — The Death of Classic OpenLane (v0.23)

This document exists for one reason:

> **To permanently close the discussion about “reviving Classic OpenLane”.**

Classic OpenLane is not deprecated.
It is not unsupported.
It is **irrecoverable**.

This is not opinion.
This is a postmortem.

---

## What “Classic OpenLane” Refers To

In this document, **Classic OpenLane** means:

- OpenLane v0.23 era (2021–2022)
- Makefile-based flow
- Pre-volare PDK handling
- sky130A PDK distributed as tarballs
- efabless/openlane Docker images with embedded PDKs
- open_pdks build inside container or host

This environment was once stable.
It is no longer reconstructible.

---

## How Classic OpenLane Actually Died

Classic OpenLane did **not** die from bugs.
It died from **ecosystem erasure**.

### 1. Docker Images Were Removed or Mutated

- `efabless/openlane:v0.23` no longer exists as originally published
- Old digests were deleted
- Tags were repointed to volare-based images
- Images with embedded sky130A PDK are gone

**Result:**  
You cannot pull a historically correct Classic container anymore.

---

### 2. sky130A PDK Tarballs Were Deleted

- GitHub Releases: removed
- S3 mirrors: removed
- Internal efabless mirrors: removed

Classic OpenLane depended on **exact PDK snapshots**.
Those snapshots no longer exist.

**Result:**  
Even if you had the flow, you cannot recreate the inputs.

---

### 3. open_pdks Became Unbuildable for Classic

- skywater-pdk now requires newer toolchains
- GLIBC requirements exceed Classic base images
- Conda/Miniconda assumptions changed
- Python tooling drifted

Classic OpenLane expected:
> “Build PDK from open_pdks when needed”

That path is now broken.

---

### 4. Infrastructure Assumptions Changed

- ORFS legacy images removed
- “In-a-box” education containers removed
- Dependency pinning loosened upstream
- Continuous delivery replaced archival stability

Classic OpenLane assumed **immutability**.
The ecosystem moved to **continuous change**.

---

## Why “Just Rebuild It” Is Impossible

Attempts that **do not work**:

- Rebuilding open_pdks from current master
- Mixing old flow with new PDK
- Using volare with Classic flow
- Extracting PDKs from modern containers
- Rewriting paths or scripts
- Pinning random commits retroactively

These produce:
- Silent mismatches
- Subtle LVS/DRC differences
- STA drift
- GLS failures
- False confidence

A design that “runs” is not a design that is **equivalent**.

---

## Responsibility Clarification

### This Is NOT User Error

The loss of Classic OpenLane is due to:

- Upstream asset deletion
- Infrastructure reorganization
- Non-archival distribution practices

No amount of care by an end user could prevent this,
unless they had **offline full backups** of:

- Docker images
- PDK tarballs
- Toolchains

That is not a reasonable expectation.

---

## Why This Repository Exists Because of This

This repository is a direct response to this failure.

**Lessons learned:**

- Never depend on upstream permanence
- Never assume old versions can be rebuilt later
- Never rely on “I can always reinstall”
- Treat environments as **artifacts**, not setups

---

## The Only Valid Replacement Strategy

Classic OpenLane cannot be restored.

What *can* be done:

- Use OpenLane1 (current Makefile-based) as a stable baseline
- Pin exact tool + PDK combinations
- Avoid rebuilding PDKs
- Avoid conda-based flows
- Use WSL export/import as the primary backup mechanism
- Freeze working environments

This reproduces **functionality**, not history.

That is sufficient.
And that is the only realistic goal.

---

## Final Verdict

Classic OpenLane is dead.

Not deprecated.  
Not broken.  
Not unsupported.

**Gone.**

Any guide suggesting otherwise is misleading you.

This repository exists so you never have to learn this the hard way again.
