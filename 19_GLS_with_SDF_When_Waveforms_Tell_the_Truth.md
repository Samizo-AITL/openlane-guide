# 19_GLS_with_SDF_When_Waveforms_Tell_the_Truth.md
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
```

Execution:

```bash
vvp sim.out +sdf_annotate+design.sdf
```

No SDF flag → no timing truth.

---

## Clock Alignment Matters

In SDF GLS:

- Clock edges are delayed
- Clock skew is real
- Launch and capture clocks differ

If your testbench assumes an ideal clock,
your results are meaningless.

Always treat the clock as part of the design.

---

## Why Waveforms Look “Ugly”

Real waveforms include:

- Glitches
- Uneven delays
- Skew-induced shifts
- Non-symmetric transitions

This is not noise.

This is reality.

Clean waveforms belong to RTL, not silicon.

---

## Common Misinterpretations

### “The waveform is broken”
No. The design is broken.

### “GTKWave looks wrong”
GTKWave is innocent.

### “RTL worked”
Irrelevant.

---

## Debugging with SDF GLS

Recommended approach:

1. Identify failing cycle
2. Trace back to register capture
3. Observe data arrival vs clock
4. Compare with STA critical path
5. Fix timing, not testbench

Never mask the symptom.

---

## When to Use SDF GLS

Use it when:

- STA shows marginal slack
- You suspect hold violations
- Functional failures appear post-route
- Verifying fixes for timing ECOs

Do **not** use it as a replacement for STA.

---

## Performance Reality

SDF GLS is slow.

This is expected.

Speed is sacrificed for correctness.

---

## Chapter Conclusion

- STA tells you timing margins
- SDF GLS shows timing behavior
- Both describe the same physics
- Disagreement means misunderstanding

If GLS and STA disagree,
you misinterpreted one of them.

---

## Next Chapter

Now that timing behavior is visible,
we address **why environments collapse**.

👉 **`20_Why_OpenLane_Environments_Break_and_How_to_Stop_It.md`**

---
