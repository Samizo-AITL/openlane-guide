# openlane-guide

> Read this repository and stop breaking your OpenLane environment forever.

This repository is a battle-tested, failure-driven guide for running OpenLane
in a stable, reproducible, and disaster-proof way.

This is not a quick-start.
This is not a feature reference.

This repository exists because real environments were broken.

---

## What this repository contains

This repository contains the **entire OpenLane reality**, including:

- WSL2 + Docker environment survival
- OpenLane1 vs OpenLane2 coexistence
- PDK asset management (sky130 / gf180)
- Full physical design flow
- Placement, CTS, Routing
- DRC / LVS / STA
- GDS signoff
- GLS (functional and SDF)
- Caravel hardening
- End-to-end RTL → GDS → GLS → MPW
- Failure cases and irreversible mistakes
- Disaster recovery by WSL export/import

Nothing here is theoretical.
Every file exists because something failed before.

---

## How to read this repository

This repository is **linear**.

You are expected to read files in order.
Skipping steps guarantees failure.

Start with:

- `INDEX.md`

---

## Core rules

- Do not fix. Roll back.
- Do not update. Clone.
- Do not rebuild. Export & import.
- Your environment is an asset, not a workspace.

If you violate these rules, failure is expected.

---

## Scope

Included:
- OpenLane1 (stable)
- OpenLane2 (evaluation-only)
- sky130 / gf180
- WSL2 + Docker Desktop
- GLS (Icarus Verilog)
- OpenROAD / OpenSTA
- Magic / KLayout
- Caravel / MPW flow

Excluded by design:
- Verilog tutorials
- ASIC theory textbooks
- Option encyclopedias
- “Latest version” workflows

---

If this repository saves you even one full reinstall,
it has already done its job.
