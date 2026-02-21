# 16_GLS_and_SDF.md
**Gate-Level Simulation and SDF — Where Logic Meets Physics**

---

## Purpose of This Chapter

The purpose of this chapter is to explain **why Gate-Level Simulation (GLS) exists**
and how it connects:

- RTL logic  
- Physical layout  
- Timing reality  

In short:

> **GLS is where “it should work” becomes “it actually works.”**

If you skip GLS, you are trusting assumptions instead of silicon reality.

---

## What GLS Really Is

GLS simulates:

- Synthesized gate-level netlists  
- Real standard cells  
- Real connectivity  

Unlike RTL simulation:

- There are no ideal registers  
- There are no implicit initial values  
- Everything starts as **X**

This is intentional.

---

## Why RTL Simulation Is Not Enough

RTL simulation assumes:

- Zero wire delay  
- Ideal clocks  
- Perfect initialization  

Silicon does **none** of these.

GLS exists to expose:

- Missing resets  
- X-propagation paths  
- Incorrect clock usage  
- Structural mismatches  

---

## Types of GLS

### 1. Functional GLS (No SDF)

- Gate-level netlist
- No timing delays
- Logic-only verification

Used to answer:

> “Does the synthesized structure behave logically?”

---

### 2. Timing GLS (With SDF)

- Gate-level netlist
- Cell delays + wire delays
- Back-annotated timing

Used to answer:

> “Does this chip work **at speed**?”

---

## Required Files for GLS

A correct GLS setup **always** requires:

- Gate-level netlist (`*.v`)
- Standard cell library (`sky130_fd_sc_hd.v`)
- Primitive definitions (`*_primitives.v`)
- Testbench
- Optional: SDF file

Missing **any** of these guarantees failure.

---

## Why Everything Becomes X

At gate level:

- Flip-flops have no defined power-up state
- Latches start unknown
- Combinational loops amplify X

This is not a bug.

> **X is telling you the truth.**

---

## The Role of Reset Signals

A correct design must:

- Assert reset explicitly
- Hold reset long enough
- Release reset cleanly

If GLS shows X forever:

> The design is wrong, not the simulator.

---

## Common GLS Failure Patterns

### Pattern 1: All-X Waveforms

**Cause**
- Missing reset
- Wrong library loading
- Wrong top module

**Meaning**
- Simulation cannot resolve logic

---

### Pattern 2: Unknown Module Errors

**Cause**
- Missing primitive library
- Incorrect include order

**Meaning**
- Simulator cannot build the circuit

---

### Pattern 3: RTL Works, GLS Fails

**Cause**
- Uninitialized signals
- Implicit latches
- Clock misuse

**Meaning**
- RTL relied on ideal assumptions

---

## Why SDF Changes Everything

SDF introduces:

- Gate delays
- Wire delays
- Clock skew
- Hold/setup violations

This transforms simulation from
**logical correctness** to **timing correctness**.

---

## Setup vs Hold in Simulation

With SDF:

- Setup violations cause wrong data capture
- Hold violations cause race conditions

These appear as:
- Glitches
- Unexpected transitions
- Intermittent failures

Exactly like real silicon.

---

## Why SDF GLS Is Rarely Used (and Why It Matters)

Many flows skip SDF GLS because:

- It is slow
- It is painful
- It exposes real problems

That is precisely why it matters.

---

## Relationship Between STA and GLS

- STA predicts timing mathematically
- GLS demonstrates timing behavior dynamically

They should agree.

If they do not:

> **Trust GLS. Fix the design.**

---

## Practical Completion Criteria

GLS is considered successful only if:

- Functional GLS passes
- Timing GLS behaves as expected
- No persistent X propagation
- Reset behavior is clean

Anything less is unfinished.

---

## Chapter Conclusion

- GLS is not optional verification
- X-propagation is a feature, not a bug
- SDF exposes real silicon behavior
- RTL correctness does not imply chip correctness

---

## Next Chapter

Next, we return to the physical world.

👉 **`17_Magic_KLayout_Reality_Check.md` — Reading the Truth from GDS**

---
