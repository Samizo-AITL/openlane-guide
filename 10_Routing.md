# 10_Routing.md  
**Routing — This Is Not a Solver**

---

## Purpose of This Chapter

Routing is where many people expect miracles.

They should not.

Routing does **not**:
- fix timing
- fix placement
- fix CTS
- fix bad design decisions

Routing only answers one question:

> **Can this design be physically connected without violating rules?**

If the answer is “no”, the design was already broken earlier.

---

## What Routing Actually Does

Routing takes:
- placed cells
- a clock tree
- legal metal layers
- spacing and width rules

and attempts to:
- connect all nets
- obey DRC rules
- minimize congestion

That is all.

---

## Routing Phases in OpenROAD

### 1. Global Routing
- estimates routing paths
- builds congestion maps
- does not draw exact wires

This phase answers:
> “Is routing even possible?”

---

### 2. Detailed Routing
- creates real wires
- inserts vias
- enforces all DRC rules

This phase answers:
> “Can it be routed legally?”

---

## The Single Most Important Rule

> **If global routing looks bad, stop.**

Do not proceed to detailed routing.

Detailed routing will not fix congestion.
It will only fail later and harder.

---

## Reading Global Routing Results

You must look at:
- congestion heat maps
- overflow reports
- hot spots

Red flags:
- severe congestion near clock spines
- long narrow channels
- dense standard-cell clusters

These indicate placement or floorplan failure.

---

## Common Routing Failure Patterns

### Pattern 1: Overflow everywhere

**Cause:**
- too small core area
- too aggressive utilization
- poor pin placement

**Correct action:**
- rollback
- fix floorplan

---

### Pattern 2: Routing completes but DRC explodes

**Cause:**
- metal spacing violations
- via density problems
- antenna issues

**Correct action:**
- analyze rule type
- fix root cause (not router settings)

---

### Pattern 3: Routing completes but timing collapses

**Cause:**
- routing added delay to already-bad paths

**Correct action:**
- timing should have been fixed before routing

---

## Antenna Violations (Do Not Ignore)

Antenna violations are:
- not cosmetic
- not optional
- not safe to waive blindly

They indicate:
- real manufacturing risks

Fix them structurally or with proper diode insertion.

---

## Routing vs Timing Reality

Routing **always increases delay**.

If timing was barely passing before routing:
it will fail after routing.

This is normal and expected.

---

## What NOT to Do During Routing

- Do not increase router effort blindly
- Do not ignore congestion warnings
- Do not treat DRC as optional
- Do not keep routing “until it passes”

Routing failure means **earlier failure**.

---

## Healthy Routing Indicators

A healthy routing stage shows:
- low congestion
- limited DRC violations
- predictable timing degradation
- stable memory usage

If routing feels “fragile”:
it is.

---

## Output Artifacts After Routing

You should get:
- routed DEF
- clean or manageable DRC
- SPEF for STA
- GDS-ready layout

If any of these are missing:
rollback.

---

## Why This Chapter Exists

Routing does not reward optimism.

It punishes earlier mistakes.

Treat routing as a validation step, not a repair tool.

---

## Next Chapter

If routing is clean:

- **`11_STA.md` — Timing Is a Contract, Not a Guess**

---
