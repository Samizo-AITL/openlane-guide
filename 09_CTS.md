# 09_CTS.md  
**Clock Tree Synthesis — Where Timing Becomes Real**

---

## Purpose of This Chapter

Clock Tree Synthesis (CTS) is the point where:

- ideal clocks stop existing
- real delays appear
- timing problems become visible
- many designs silently fail

If placement decides *whether* a design can work,  
CTS decides *whether it actually does*.

This chapter explains:
- what CTS really builds
- why CTS failures are design failures
- how to read CTS results
- what *cannot* be fixed after CTS

---

## What CTS Does

CTS takes:
- an ideal clock
- placed sequential elements (FFs)

and builds:
- a **real clock network**
- with buffers, inverters, and routing
- obeying physical constraints

The result is:
- clock latency
- clock skew
- clock insertion delay

From this point on, **timing is no longer abstract**.

---

## What CTS Does NOT Do

CTS does NOT:
- fix bad placement
- fix unrealistic clock periods
- fix logic depth problems
- magically remove skew

CTS only works if everything before it was sane.

---

## Clock Concepts You Must Understand

### Clock Latency
Time from clock source to a flip-flop.

### Clock Skew
Difference in arrival time between two flip-flops.

### Insertion Delay
Total delay added by the clock tree itself.

CTS trades off:
- latency
- skew
- buffer count
- power

You do not get all of them “perfect”.

---

## CTS in OpenLane / OpenROAD

OpenLane uses OpenROAD’s TritonCTS.

Typical flow position:
- after placement
- before routing

If CTS fails, routing should not be attempted.

---

## Common CTS Failure Symptoms

### Symptom 1: CTS does not converge

- endless buffering
- excessive levels
- tool aborts

**Cause:**  
Placement congestion or unrealistic clock targets.

---

### Symptom 2: Massive clock skew

- hold violations everywhere
- timing impossible to close

**Cause:**  
Unbalanced placement or extreme distances.

---

### Symptom 3: Clock buffers explode

- power skyrockets
- routing congestion increases

**Cause:**  
Clock trying to compensate for poor placement.

---

## Why CTS Is a Placement Quality Test

CTS is the first consumer of placement quality.

If placement has:
- dense regions
- long distances
- narrow channels

CTS will expose it brutally.

This is expected behavior.

---

## What to Inspect After CTS

You must inspect:

- clock buffer count
- maximum clock depth
- skew values
- latency range

Red flags:
- very deep clock trees
- extreme skew (> few hundred ps in sky130)
- clock buffers dominating area

---

## CTS and Timing (STA Starts Here)

After CTS:
- setup timing becomes meaningful
- hold problems appear
- clock uncertainty matters

If timing is catastrophic here:
**do not proceed to routing**.

Routing will only make it worse.

---

## What NOT to Do

- Do not tighten clock period blindly
- Do not ignore skew reports
- Do not push CTS effort hoping for miracles
- Do not “let routing fix timing”

CTS is not a repair stage.

---

## Practical Rules That Work

- Fix placement before CTS
- Use realistic clock periods
- Treat CTS failure as design failure
- Stop early if CTS looks unhealthy

---

## Output Artifacts After CTS

A healthy CTS produces:
- a clocked DEF
- reasonable skew
- controlled buffer insertion
- no explosion in congestion

If not:
**rollback**.

---

## Why This Chapter Exists

Many designs “pass placement” and die silently at CTS.

That is not bad luck.
That is physics.

CTS tells you whether your design deserves to continue.

---

## Next Chapter

Proceed only if CTS is clean.

Next:
- **`10_Routing.md` — Routing Is Not a Solver**
---
