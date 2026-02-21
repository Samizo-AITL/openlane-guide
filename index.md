# OpenLane Guide — Repository Index

This repository is intentionally **linear**.  
Do not treat it as a reference dump.

If you read these documents **in order**, you will end with a
**stable, reproducible, and portable OpenLane environment**.

If you do not, you will break something.

---

## Required Reading Order

### 01 — Foundation (Do not skip)
- **01_WSL_Docker_Setup.md**  
  Establishes a WSL2 + Docker environment that can survive export/import.  
  No OpenLane yet. Stability first.

### 02 — Stable Production Flow
- **02_OpenLane1_Setup.md**  
  Installs and *freezes* OpenLane1.  
  This is the production-grade flow.  
  Updates are explicitly discouraged.

### 03 — Evaluation-Only Flow
- **03_OpenLane2_Setup.md**  
  OpenLane2 setup for experimentation only.  
  Strict isolation rules are enforced.  
  Never mix with OpenLane1.

### 04 — The Asset
- **04_PDK_Setup.md**  
  sky130 / gf180 PDK setup.  
  This is the most expensive and fragile asset.  
  Built once. Never rebuilt.

### 05 — Proof of Correctness
- **05_Verification_Test.md**  
  Smoke tests to confirm:
  - OpenLane completes
  - PDK is correctly referenced
  - Toolchain is intact

### 06 — Disaster Recovery
- **06_Migration_WSL_Export.md**  
  Export / import strategy for WSL.  
  Hardware failure becomes irrelevant.

### 07 — Failure Prevention
- **07_Troubleshooting.md**  
  Not a fix-it guide.  
  A checklist for **never breaking the environment again**.

---

## Design Philosophy (Non-Negotiable)

- Do not fix → **roll back**
- Do not update → **clone**
- Do not rebuild → **export/import**
- The environment is an **asset**, not a workspace

If you violate these rules, failure is expected.

---

## What This Repository Guarantees

If followed exactly:

- OpenLane runs end-to-end
- GLS works (no unknown modules, no all-X)
- STA / OpenROAD are usable
- PDK mismatch errors disappear
- Environment migration takes minutes, not days

If something breaks:
**you deviated from the process**.

---

## Scope (Explicit)

Included:
- OpenLane1
- OpenLane2 (isolated)
- sky130 / gf180
- WSL2 + Docker Desktop
- GLS (Icarus Verilog)
- OpenROAD / OpenSTA
- Magic / KLayout
- WSL export/import disaster recovery

Excluded by design:
- Verilog tutorials
- ASIC theory
- Option encyclopedias
- “Latest version” workflows

---

## Final Warning

This repository is not friendly.  
It is not flexible.  
It is not modern.

It is **reliable**.

If you want novelty, look elsewhere.  
If you want OpenLane to stop breaking, stay here.
