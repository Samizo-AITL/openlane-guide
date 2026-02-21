# APPENDIX — GLS Failure Patterns (Sky130 / OpenLane)

This document catalogs **recurring Gate-Level Simulation (GLS) failures**
observed in real OpenLane environments.

The goal is not to explain GLS theory,
but to **eliminate dead ends and false debugging paths**.

If GLS fails, it almost always fails in **predictable ways**.

---

## Scope

This appendix applies to:

- OpenLane1 / OpenLane2
- sky130_fd_sc_hd standard cells
- Icarus Verilog (iverilog + vvp)
- Functional GLS and SDF-annotated GLS
- WSL2 + Linux native environments

---

## Pattern 1: “Unknown module” (Hundreds of Errors)

### Typical Symptoms

```text
error: Unknown module type: sky130_fd_sc_hd__dfxtp_1
error: Unknown module type: sky130_fd_sc_hd__inv_2
