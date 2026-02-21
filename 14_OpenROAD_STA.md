# 14_OpenROAD_STA.md  
**Static Timing Analysis with OpenROAD — Reading Timing Like a Professional**

---

## Purpose of This Chapter

This chapter exists for one reason:

> **To make STA reports readable, actionable, and non-mystical.**

Many users can *run* OpenSTA.  
Very few can *read* its output correctly.

After this chapter, STA stops being noise.

---

## What STA Actually Proves

Static Timing Analysis answers this question:

> **Is every signal guaranteed to arrive on time, under worst conditions?**

STA does **not** simulate behavior.  
STA assumes **all possible paths** exist.

This makes STA:
- conservative
- pessimistic
- brutally honest

---

## STA vs Simulation

| Aspect | Simulation | STA |
|----|----|----|
| Stimulus | Required | Not needed |
| Coverage | Limited | Exhaustive |
| Speed | Slow | Fast |
| Optimism | High | None |

Simulation shows *what happened*.  
STA proves *what can never fail*.

---

## OpenROAD STA Toolchain

OpenLane uses:

- OpenROAD
- OpenSTA (integrated)

Inputs:
- synthesized netlist
- extracted parasitics (SPEF)
- liberty timing models
- SDC constraints

If any input is wrong, STA lies.

---

## Required Files for STA

A valid STA run requires:

- `.v` (gate-level netlist)
- `.lib` (standard cell timing)
- `.sdc` (constraints)
- `.spef` (interconnect parasitics)

Missing one = meaningless result.

---

## Understanding Slack (The Core Metric)

Slack = **required time − arrival time**

| Slack | Meaning |
|----|----|
| Positive | Safe |
| Zero | Barely legal |
| Negative | Failure |

Slack is the only number that matters.

---

## Setup vs Hold (Do Not Confuse Them)

### Setup
- data arrives **too late**
- clock frequency too high
- long paths

### Hold
- data arrives **too early**
- clock skew issue
- short paths

They are unrelated problems.

Fixing setup can break hold.

---

## Worst Negative Slack (WNS)

WNS answers:

> **How bad is the single worst path?**

- WNS < 0 → design fails
- WNS = 0 → knife edge
- WNS > 0 → margin exists

Never ignore WNS.

---

## Total Negative Slack (TNS)

TNS answers:

> **How many problems exist overall?**

- small WNS + huge TNS → many small issues
- large WNS + small TNS → one critical path

Both matter.

---

## Path Reports: How to Read Them

A timing path consists of:

1. launch clock
2. clock-to-Q
3. combinational logic
4. interconnect delay
5. setup requirement

Read paths **top to bottom**, not backward.

---

## Common Beginner Mistake

Looking only at:
```
Slack: +0.12ns
```

Without checking:
- clock uncertainty
- constraint correctness
- false path assumptions

Positive slack does not guarantee correctness.

---

## Clock Definition Is Everything

STA quality depends on clock modeling:

- clock period
- waveform
- uncertainty
- generated clocks
- clock groups

Bad clocks = fake success.

---

## False Paths and Multicycle Paths

Used incorrectly, they:
- hide real violations
- produce false confidence

Rule:
> **Only declare false paths you can physically justify.**

Never use them to silence STA.

---

## Correlating STA and SDF GLS

Correct flow:

1. STA identifies worst paths
2. SDF GLS confirms behavior
3. Both agree

If they disagree:
- hierarchy mismatch
- wrong constraints
- or testbench lies

Never trust only one.

---

## Why Designers Fear STA

Because STA:
- exposes shortcuts
- ignores intent
- punishes assumptions

This is exactly why it must be trusted.

---

## Professional Mindset

Do not ask:
> “How do I make STA pass?”

Ask:
> “What is STA trying to tell me?”

The answer is usually correct.

---

## When STA Is Finished

STA is finished when:

- no negative slack
- margins are intentional
- constraints are reviewed
- SDF GLS agrees

Not earlier.

---

## Why This Chapter Matters

Most OpenLane failures blamed on tools are:
- constraint errors
- clock misunderstandings
- STA misinterpretation

This chapter prevents that.

---

## Next Chapter

After timing mastery:

- **`15_Routing_and_Congestion.md` — When Wires Decide Everything**

---
