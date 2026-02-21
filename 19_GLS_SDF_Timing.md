# 19_GLS_SDF_Timing
**Timing in Motion**

---

## Purpose of This Chapter

This chapter explains **why Gate-Level Simulation (GLS) with SDF**
is the **only place where timing becomes visible as behavior**.

STA tells you *that* timing fails.  
**SDF-annotated GLS shows you *how* it fails.**

Both are required to understand real silicon behavior.

---

## What SDF-Backannotated GLS Actually Is

SDF (Standard Delay Format) contains:

- Cell delays
- Interconnect delays
- Setup / hold checks
- Timing arcs resolved from STA

When applied to GLS:

- Every gate delay is real
- Every wire delay is real
- Violations manifest as **wrong waveforms**

This is no longer logic simulation.  
It is **time simulation**.

---

## Why Plain GLS Is Not Enough

Plain GLS (without SDF):

- Verifies structural correctness
- Catches X-propagation issues
- Confirms reset behavior

But it **lies about timing**.

Without SDF:
- Zero-delay gates
- Ideal wires
- Unrealistic alignment

It is necessary, but insufficient.

---

## What SDF GLS Reveals That STA Cannot

STA reports:
- Numbers
- Paths
- Margins

SDF GLS reveals:
- Glitches
- Metastability windows
- Race conditions
- Functional corruption due to timing

STA says *why*.  
GLS shows *what happens*.

---

## Typical Failure Signatures in SDF GLS

### Setup Violation Symptoms

- Data arrives late
- Register captures old value
- Output lags one cycle behind
- Silent functional failure

### Hold Violation Symptoms

- Output toggles unexpectedly
- Glitches after clock edge
- Non-deterministic behavior
- Appears “random”

Hold violations are especially dangerous
because they often look like logic bugs.

---

## How SDF Is Applied in Practice

Typical invocation:

```bash
iverilog -g2012 -DSDF_ANNOTATE \
  sky130_fd_sc_hd__primitives.v \
  sky130_fd_sc_hd.v \
  design.gl.v tb.v \
  -o sim.out
