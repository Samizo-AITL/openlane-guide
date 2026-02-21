# 11_STA.md  
**Static Timing Analysis — Timing Is a Contract**

---

## Purpose of This Chapter

Static Timing Analysis (STA) is not a suggestion system.

It is a **contract**.

If STA says the design does not meet timing,
the design is **invalid**, regardless of simulations or intentions.

---

## What STA Actually Answers

STA answers one question only:

> **Will every signal arrive before it is required, under worst-case assumptions?**

It does not simulate behavior.
It does not care about functional correctness.

It only cares about **time**.

---

## The Timing Contract

Every timing path is defined by:

- launch clock edge
- data path delay
- capture clock edge
- required arrival time

If:

```
arrival_time ≤ required_time
```

The path passes.

If not, the chip fails.

---

## Key STA Terms (No Hand-Waving)

### Setup Slack
- measures if data arrives **too late**
- negative slack = failure

### Hold Slack
- measures if data arrives **too early**
- negative slack = failure

Both matter.
Passing setup but failing hold is still failure.

---

## Why Simulation Cannot Replace STA

Simulation:
- checks specific scenarios
- depends on testbench coverage
- ignores worst-case corners

STA:
- checks **all paths**
- assumes worst-case delay
- is corner-aware

Real silicon obeys STA, not simulation optimism.

---

## Reading STA Reports Correctly

Never start with averages.

Always start with:
- worst negative slack (WNS)
- total negative slack (TNS)
- top failing paths

If WNS < 0:
stop.

---

## The Most Common STA Mistake

> “It only fails by a little.”

There is no “a little” in silicon.

A −10 ps violation is as real as −1 ns.

---

## Clock-Related Failures

Clock problems dominate STA failures:

- excessive clock skew
- poor CTS structure
- unbalanced clock trees

Fix clocks first.
Always.

---

## Data Path Failures

Common causes:
- long combinational chains
- excessive fanout
- poor placement
- routing detours

These are architectural problems, not tool problems.

---

## Hold Violations Are Not Optional

Hold violations:
- cannot be masked
- cannot be fixed by frequency reduction
- must be fixed structurally

Ignoring hold violations guarantees silicon failure.

---

## STA Before and After Routing

Pre-route STA:
- optimistic
- used for guidance

Post-route STA:
- reality
- final authority

Only post-route STA matters.

---

## What STA Is Not

- not a tuning exercise
- not a report-generation task
- not optional
- not negotiable

STA is the law.

---

## When to Roll Back

Immediately roll back if:
- WNS worsens after routing
- new violations appear unexpectedly
- CTS changes destabilize timing

Fix the cause, not the report.

---

## Healthy STA Indicators

A healthy design shows:
- positive WNS
- small TNS
- stable results across runs
- predictable corner behavior

Anything else is a warning.

---

## Why This Chapter Exists

Many designs “work” in simulation.

They still fail in silicon.

STA is how silicon speaks back.

---

## Next Chapter

After timing is clean:

- **`12_GLS.md` — Logic Meets Reality**

---
