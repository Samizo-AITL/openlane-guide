# 08_Placement.md  
**Placement — Where Most OpenLane Designs Actually Fail**

---

## Purpose of This Chapter

Placement is the first stage where **logical correctness meets physical reality**.

Most OpenLane failures that appear later as:
- routing explosions
- CTS failures
- negative slack everywhere
- DRC hell

are **already decided at placement time**.

This chapter explains:
- what placement really does
- why “it placed successfully” means nothing
- how to read congestion and density
- what *bad placement* looks like before it ruins everything

---

## What Placement Is (and Is Not)

### Placement IS:
- Assigning **exact physical locations** to standard cells
- Balancing **density, wirelength, and routability**
- Preparing the design for CTS and routing

### Placement is NOT:
- Just “put cells somewhere”
- A step you can ignore because routing will fix it
- Independent from timing

Once placement is bad, **nothing later can save you**.

---

## Placement Stages in OpenLane / OpenROAD

OpenLane uses OpenROAD’s placement engines.

### 1. Global Placement (GPL)

- Rough cell distribution
- Optimizes:
  - wirelength
  - density
- Ignores exact legal positions

Output:
- Density maps
- Initial congestion hints

### 2. Detailed Placement (DPL)

- Legalizes cell positions
- Fixes overlaps
- Aligns to rows and sites

**DPL cannot fix bad GPL decisions.**

---

## Running Placement (Context)

You normally do **not** run placement manually in OpenLane1.
It is executed as part of the flow.

However, understanding where it happens matters.

Typical log sections:
- `global placement`
- `detailed placement`

If placement fails, everything stops here.

---

## The Most Important Concept: Density

### What is density?

Density =  
> how much cell area is packed into a region

Too low:
- long wires
- timing issues

Too high:
- routing congestion
- DRC violations
- CTS failure

### Typical safe density

For sky130:
- ~60–70% is reasonable
- >75% is dangerous
- >80% is usually fatal

---

## Congestion Is Not a Routing Problem (Yet)

Congestion at placement stage means:
- too many cells competing for routing tracks
- later routing **will fail**, guaranteed

Placement congestion is a **design problem**, not a router problem.

---

## How to Inspect Placement Visually

### Using OpenROAD GUI

```sh
openroad -gui
```

Load:
- LEF
- DEF after placement

Look for:
- red / hot congestion areas
- dense cell clusters
- long thin placement shapes

If you see:
- big empty areas
- dense corners
- diagonal clustering

👉 placement is already broken.

---

## Common Placement Failure Patterns

### Pattern 1: Over-packed core

Symptoms:
- routing fails everywhere
- CTS reports impossible skew
- DRC floods

Cause:
- core utilization too high
- unrealistic floorplan

Fix:
- lower utilization
- increase core area

---

### Pattern 2: Macro blindness (OpenLane2 / Caravel)

Symptoms:
- cells squeezed around macros
- local congestion walls

Cause:
- macro blockages ignored or misconfigured

Fix:
- explicit macro placement
- proper halos and blockages

---

### Pattern 3: Long critical paths

Symptoms:
- WNS very negative
- timing never recovers

Cause:
- related logic placed far apart

Fix:
- hierarchy
- constraints
- sometimes RTL changes

---

## Placement and Timing Are Already Linked

Even before CTS:
- wirelength affects delay
- placement affects slew
- congestion affects buffering

If timing is bad later:
**placement probably caused it**.

---

## What NOT to Do

- Do not increase router effort to “fix” placement
- Do not ignore congestion warnings
- Do not assume CTS will solve it
- Do not push utilization “just to see”

Placement is not forgiving.

---

## Practical Rules That Actually Work

- Start with conservative utilization
- Watch congestion early
- Fix placement before routing
- Treat placement failure as design failure

---

## Output Artifacts After Placement

After successful placement you should have:
- DEF with legal cell placement
- Reasonable congestion maps
- No overlap errors
- No extreme density hotspots

If any of these are missing:
**stop here**.

---

## Why This Chapter Exists

Most OpenLane guides jump from synthesis to routing.

That is why most OpenLane designs fail.

Placement decides:
- whether routing is possible
- whether CTS will converge
- whether STA has a chance

Everything after this chapter is downstream damage control.

---

## Next Chapter

Continue only if placement is clean.

Next:
- **`09_CTS.md` — Clock Tree Synthesis**
