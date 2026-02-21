# 12_GLS.md  
**Gate-Level Simulation — Logic After Reality Check**

---

## Purpose of This Chapter

Gate-Level Simulation (GLS) exists to answer one question only:

> **Does the synthesized, cell-level design still behave correctly?**

RTL simulation proves intent.  
GLS proves **implementation**.

If GLS fails, the design is **not trustworthy**, even if RTL passed.

---

## What GLS Actually Verifies

GLS verifies:

- synthesized netlist behavior
- real standard-cell logic
- reset correctness
- X-propagation issues
- mismatch between RTL and synthesis

GLS does **not** care about performance.  
That is STA’s job.

---

## RTL vs GLS: The Critical Difference

### RTL Simulation
- ideal registers
- perfect logic
- no cell-level detail

### GLS
- real flip-flops
- real gates
- real unknown (X) behavior

If something is ambiguous, GLS will expose it.

---

## Why GLS Fails When RTL Passes

Common reasons:

- missing or incorrect reset
- inferred latches
- uninitialized registers
- reliance on simulator-specific behavior
- synthesis optimizations changing structure

RTL hides these.
GLS does not.

---

## Mandatory Inputs for GLS (sky130)

GLS **will not work** unless all of the following are present:

- synthesized gate-level netlist
- sky130 standard-cell Verilog models
- UDP primitives (flip-flops, latches, muxes)
- correct compile order

Missing even one guarantees failure.

---

## The #1 GLS Failure: “Unknown Module”

Symptoms:
- hundreds of errors
- `unknown module sky130_*`

Cause:
- standard-cell libraries not loaded
- primitives not included
- wrong PDK path

This is not a Verilog bug.
It is an environment bug.

---

## The #2 GLS Failure: All-X Waveforms

Symptoms:
- outputs stuck at X
- internal signals unknown

Causes:
- reset not asserted
- reset too short
- relying on initial values
- missing `$dumpvars` depth

GLS requires **explicit reset discipline**.

---

## Reset Discipline Rules

In GLS:

- all registers start as X
- reset must be asserted
- reset must be long enough
- reset must reach all flops

If reset is optional, GLS will punish you.

---

## Compile Order Is Not Optional

Correct order (example):

1. UDP primitives
2. standard-cell functional models
3. gate-level netlist
4. testbench

Any other order is wrong.

Icarus Verilog does not guess.
Neither should you.

---

## Functional vs Timing GLS

### Functional GLS
- ignores delays
- checks logic correctness

### Timing GLS (SDF)
- includes cell and interconnect delays
- exposes race conditions
- correlates with STA

Always start with functional GLS.
Timing GLS comes later.

---

## When GLS Is Mandatory

GLS is mandatory when:

- taping out
- handing design to others
- verifying reset logic
- debugging synthesis differences

Skipping GLS is a gamble.
Silicon never forgives gambles.

---

## When GLS Is Optional

GLS may be skipped only if:

- design is trivial
- reset behavior is proven
- synthesis is well-understood
- risk is acceptable

Even then, skipping GLS is a decision — not an omission.

---

## The GLS Mindset

If GLS fails:

- do not patch the testbench
- do not mask X values
- do not ignore warnings

Fix the design.

GLS is not wrong.
Your assumptions are.

---

## Why This Chapter Exists

Most OpenLane users fail at GLS.

Not because GLS is hard —  
but because environments are broken and rules are ignored.

This guide exists so GLS becomes boring.

---

## Next Chapter

Once GLS is clean:

- **`13_SDF_GLS.md` — Timing Meets Logic**

---
