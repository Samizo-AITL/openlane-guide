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
```

Often followed by:

- 500+ errors
- Simulation aborts immediately

---

### Root Cause

**Standard cell definitions are not loaded.**

Specifically, one or more of the following is missing:

- `sky130_fd_sc_hd.v`
- `sky130_fd_sc_hd__primitives.v`
- UDP primitive files (`*_udp_*.v`)

GLS **cannot infer standard cells**.  
They must be explicitly provided.

---

### Corrective Action

Always include **both** files, in this order:

```bash
iverilog \
  sky130_fd_sc_hd__primitives.v \
  sky130_fd_sc_hd.v \
  design_gl.v \
  tb.v
```

> If `primitives.v` is missing, GLS will never work.

---

## Pattern 2: Simulation Runs but Everything Is `X`

### Typical Symptoms

- Simulation completes
- VCD is generated
- All signals remain `X`
- Clock toggles, but outputs never resolve

---

### Root Causes

This failure has **multiple independent causes**.

#### Cause A: No Reset Applied

Gate-level netlists start with **undefined state**.

Without reset:

- Flip-flops remain `X`
- Combinational logic propagates `X`

---

#### Cause B: `$dumpvars` Scope Too Shallow

```verilog
$dumpvars(1, tb);
```

This only dumps top-level signals.  
The DUT remains invisible.

---

#### Cause C: Wrong Netlist Used

Using:

- RTL netlist instead of gate-level netlist
- Synthesis netlist when routing-level netlist is expected

---

### Corrective Actions

Mandatory checklist:

```verilog
// Reset must be asserted
rst = 1;
#20;
rst = 0;

// Dump everything
$dumpvars(0, tb);
```

And confirm:

- DUT is the **gate-level** netlist
- Not RTL
- Not behavioral model

---

## Pattern 3: GLS Works, SDF GLS Fails

### Typical Symptoms

- Functional GLS works
- Adding SDF causes:
  - Timing violations
  - Simulation abort
  - Signals stuck
  - Massive warnings

---

### Root Causes

- SDF file does not match netlist
- Wrong hierarchy path in `$sdf_annotate`
- Mismatch between synthesis vs routing netlist
- Incorrect timescale assumptions

---

### Corrective Actions

1. Confirm **netlist source**  
   SDF must match the exact netlist used.

2. Use explicit annotation:

```verilog
$sdf_annotate(
  "design.sdf",
  dut,
  ,
  ,
  "MAXIMUM"
);
```

3. Match timescale:

```verilog
`timescale 1ns/1ps
```

---

## Pattern 4: “It Works on One Machine but Not Another”

### Typical Symptoms

- GLS works on PC A
- Same files fail on PC B
- No obvious differences

---

### Root Cause

**PDK mismatch.**

Common scenarios:

- Different sky130 versions
- Missing UDP primitives on one system
- PDK partially copied
- `/mnt/c` vs WSL filesystem differences

---

### Corrective Action

- Use a **single PDK source**
- Keep PDK inside WSL (`~`)
- Never mix Windows and Linux PDK paths
- Prefer WSL export/import for portability

---

## Pattern 5: Chasing the Wrong Problem

### Typical Mistakes

- Modifying RTL to fix GLS
- Editing standard cell models
- Rewriting netlists
- “Trying random flags”

These actions **mask the real issue**.

---

### Correct Mental Model

GLS failures are almost never:

- RTL bugs
- Tool bugs

They are almost always:

- Missing files
- Wrong file order
- Environment mismatch
- Reset / dump scope mistakes

---

## Golden Rules for GLS

1. **GLS is deterministic**
2. If it fails, the environment is wrong
3. Debug inputs, not outputs
4. Never “patch” a working netlist
5. Fix the setup, not the design

---

## Why This Appendix Exists

GLS failures are frustrating because they feel mysterious.

They are not.

Once these patterns are understood,
GLS becomes **boring and reliable**.

That is exactly what you want.
