# 17_Magic_KLayout_Reality_Check.md
**Reading Physical Truth from GDS**

---

## Purpose of This Chapter

This chapter explains how to **read reality from layout data**.

Not theory.  
Not intent.  
Not RTL.

> **GDS is what will be fabricated. Everything else is a guess.**

Magic and KLayout are not viewers.
They are truth inspectors.

---

## Why GDS Is the Final Authority

By the time GDS is generated:

- RTL assumptions are gone
- Synthesis abstractions are gone
- Timing estimates are frozen
- Physical constraints dominate

If something is wrong in GDS:

> **The chip is wrong.**

No simulator can fix that.

---

## Roles of the Tools

### KLayout — Visual Truth

KLayout is best for:

- Fast GDS inspection
- Layer visibility control
- Hierarchy navigation
- Presentation and review

KLayout answers:

> “What does the chip look like?”

---

### Magic — Physical Truth

Magic is best for:

- DRC correctness
- Layer semantics
- Transistor-level understanding
- LVS preparation
- Physical edits (if unavoidable)

Magic answers:

> “Is this layout physically valid?”

---

## Why Both Are Required

KLayout shows you *what is there*.  
Magic explains *what it means*.

Using only one guarantees blind spots.

---

## Understanding Abstract vs Real Geometry

OpenLane-generated GDS is **abstracted**:

- Standard cells are black boxes
- Internal transistor geometry is hidden
- Routing is real, devices are abstract

This is expected.

To see real devices:

- Open standard cell GDS directly
- Use Magic with PDK tech files

---

## Standard Cell Reality Check

Inspecting standard cells reveals:

- Actual transistor placement
- Poly orientation
- Diffusion sharing
- Well structure
- Power rail integration

This explains:

- Cell height constraints
- Routing limitations
- Timing behavior
- Density limits

---

## Power Distribution Inspection

GDS inspection must confirm:

- VDD/VSS rails exist
- Straps connect correctly
- No floating wells
- Tap cells are present

Power bugs do not show in RTL.
They destroy silicon silently.

---

## Clock Routing Reality

From GDS you can verify:

- Clock tree topology
- Buffer insertion
- Clock shielding
- Skew-inducing geometry

This explains why STA reports what it reports.

---

## DRC Is Not Optional

A clean flow **must** satisfy:

- Magic DRC = 0
- No waived errors
- No “expected violations”

If DRC is ignored:

> **Yield becomes zero.**

---

## LVS as Reality Confirmation

LVS answers exactly one question:

> “Is this layout the same circuit as the netlist?”

If LVS fails:

- Functionality is undefined
- Simulation results are irrelevant

---

## Common Layout Misconceptions

### Misconception 1: “It passed simulation, so it’s fine”

False.

Simulation does not see:
- Antenna effects
- Spacing rules
- Density rules
- Well continuity

---

### Misconception 2: “GDS looks fine visually”

False.

Visual symmetry does not imply:
- DRC correctness
- Electrical connectivity
- LVS correctness

---

## When Manual Edits Are Justified

Manual layout edits should be:

- Rare
- Minimal
- Fully understood

If you edit GDS without understanding PDK rules:

> **You are guessing at silicon physics.**

---

## Practical Inspection Checklist

Before trusting a GDS:

- Layers toggle correctly
- Power rails are continuous
- Clock routes are sensible
- No unexpected geometry
- DRC = clean
- LVS = match

Anything missing invalidates the chip.

---

## Chapter Conclusion

- GDS is the final truth
- KLayout shows structure
- Magic explains physics
- DRC and LVS are mandatory
- Visual comfort is irrelevant

---

## Next Chapter

Now that layout truth is understood,
we address timing truth.

👉 **`18_STA_Reality_and_Timing_Closure.md` — When Slack Becomes Law**

---
