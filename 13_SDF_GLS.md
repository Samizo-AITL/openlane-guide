# 13_SDF_GLS.md  
**SDF Back-Annotated GLS — When Timing Becomes Reality**

---

## Purpose of This Chapter

This chapter answers a single, critical question:

> **Does the design still work when real delays are applied?**

RTL simulation ignores delay.  
Functional GLS ignores delay.  

**SDF-annotated GLS does not.**

This is where logic and timing finally meet.

---

## What SDF GLS Actually Verifies

SDF GLS verifies:

- cell internal delays
- interconnect delays
- setup / hold violations
- race conditions
- clock-to-Q realism
- consistency with STA results

If STA is theory,  
**SDF GLS is experimental proof.**

---

## Relationship Between STA and SDF GLS

| Tool | Role |
|----|----|
| STA | Mathematical timing proof |
| SDF GLS | Behavioral confirmation |

They must agree.

If they do not:
- constraints are wrong
- clocks are mis-modeled
- or the testbench is lying

---

## What SDF Is (and Is Not)

SDF (Standard Delay Format):

- describes delays, not logic
- annotates an existing netlist
- does not fix broken designs

SDF cannot save you.  
It can only expose reality.

---

## Prerequisites for SDF GLS

You **must** already have:

- clean functional GLS
- synthesized netlist
- generated SDF from OpenLane
- passing STA (no fatal violations)

If functional GLS is broken,  
**do not attempt SDF GLS.**

---

## Where OpenLane Generates SDF

Typical path:

```
runs/<RUN_ID>/results/signoff/<design>.sdf
```

This SDF is derived from:
- extracted parasitics
- cell delays
- clock definitions

If this file does not exist,  
SDF GLS cannot happen.

---

## Annotating SDF in Simulation

SDF is applied at runtime.

Typical flow:

- compile netlist + libraries
- load testbench
- annotate SDF at simulation start

Annotation must target:
- correct instance
- correct hierarchy
- correct timescale

Mistakes here cause silent failure.

---

## The #1 SDF GLS Failure: “No Effect”

Symptoms:
- waveform identical to functional GLS
- no delay visible
- no violations detected

Causes:
- SDF not actually loaded
- wrong instance path
- incorrect simulation flag
- timescale mismatch

This failure is dangerous because it looks “successful”.

---

## Timescale Discipline (Critical)

SDF delays assume a timescale.

Mismatch examples:
- netlist at 1ns / testbench at 1ps
- SDF units ignored
- clock period scaled incorrectly

Rule:
> **Timescale must be consistent everywhere.**

If not, results are meaningless.

---

## Setup / Hold Violations in SDF GLS

In SDF GLS you may see:

- setup violations
- hold violations
- X-propagation after clocks

These are not simulator bugs.

They indicate:
- insufficient slack
- wrong constraints
- unrealistic clocks
- or genuine design failure

---

## Interpreting Violations Correctly

Do not panic at the first violation.

Check:

- Does STA also report it?
- Is it a real path or false path?
- Is reset being toggled near clock?
- Is the testbench realistic?

SDF GLS exposes **testbench mistakes** too.

---

## Clock Modeling Pitfalls

Common mistakes:

- ideal clock edges
- no jitter
- no uncertainty
- unrealistic duty cycle

SDF GLS punishes idealized clocks.

If your clock is fake, results are fake.

---

## When SDF GLS Is Mandatory

SDF GLS is mandatory when:

- final signoff
- clock-sensitive logic
- multiple clock domains
- asynchronous boundaries
- high-frequency operation

Skipping SDF GLS here is reckless.

---

## When SDF GLS Can Be Skipped

SDF GLS may be skipped when:

- STA margin is huge
- design is simple
- clocking is trivial
- risk is accepted

Skipping is a decision — not ignorance.

---

## The Correct Mindset

If SDF GLS fails:

- do not weaken constraints
- do not mask violations
- do not blame the tool

Fix:
- the clock
- the constraints
- or the design

Timing is physics.
Physics always wins.

---

## Why This Chapter Exists

Most designers stop at STA.

Very few confirm STA behaviorally.

Those who do:
- catch race conditions
- avoid silicon surprises
- sleep better

This chapter exists to close that gap.

---

## Next Chapter

Once timing and logic agree:

- **`14_OpenROAD_STA.md` — Reading Timing Like a Professional**

---
