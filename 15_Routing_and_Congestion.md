# 15_Routing_and_Congestion.md
**Routing and Congestion — When Wires Decide Everything**

---

## Purpose of This Chapter

The purpose of this chapter is simple:

> **Routing is not a “late-stage detail.”  
> Routing decides timing, DRC, and chip viability.**

Placement defines logical structure.  
**Routing defines whether the chip actually works.**

After this chapter, you will be able to explain:

- Why STA suddenly degrades  
- Why DRC violations explode  
- Why a GDS “looks unhealthy” at first glance  

---

## The Two-Stage Routing Model (OpenROAD)

OpenLane / OpenROAD routing always happens in two stages.

### 1. Global Routing
- Determines rough routing paths
- Estimates congestion
- **This stage decides success or failure**

### 2. Detailed Routing
- Draws actual wires
- Fixes DRC locally
- Strictly follows global routing decisions

👉  
**Detailed routing cannot save a bad global routing result.**

---

## What Is Congestion?

Congestion means:

> **The amount of wiring demanded in an area  
> exceeds the physical routing capacity.**

Logical correctness is irrelevant if wires cannot physically pass.

---

## Why Congestion Is Dangerous

High congestion inevitably causes:

- Longer wire length  
- Increased delay (STA degradation)  
- Excessive vias  
- DRC violations  
- Antenna violations  
- Uncontrolled layer usage  

👉  
**Congestion is the root cause of most physical failures.**

---

## Common Misconception

### ❌ Misconception
“Detailed routing will somehow fix it.”

### ✔ Reality
Global routing already decided the outcome.

Detailed routing only tries to make  
**an impossible design barely legal.**

---

## Viewing Congestion (OpenROAD GUI)

```bash
openroad -gui
```

Check the following:

- Global routing heatmap  
- Routing utilization  
- Congestion hotspots  

Large red regions mean  
**the design is already in trouble.**

---

## Why Congestion Happens

Typical causes include:

- Cell density too high  
- Poor floorplan  
- Bad macro or I/O placement  
- Insufficient routing layers  
- Overly aggressive PDN  

👉  
**Routing problems almost always originate upstream.**

---

## Cell Density vs Routing Tradeoff

High density:
- Shorter wires
- Less routing space

Low density:
- Longer wires
- Easier routing

👉  
**Density is always a routing tradeoff.**

---

## Why Floorplanning Dominates Routing

Floorplanning defines:

- Routing flow
- Congestion concentration
- Clock tree structure
- Power distribution paths

If routing fails,  
**the correct response is almost always to revisit the floorplan.**

---

## Clock Routing Is Special

Clock nets are:

- Longest
- Most critical
- Highest priority

Bad clock routing causes:

- Setup violations  
- Hold violations  
- Excessive skew  

👉  
**Clock routing always overrides data routing.**

---

## Layer Roles (sky130 Example)

- Metal1: intra-cell, short local wires  
- Metal2–3: local interconnect  
- Metal4–5: long wires, clock distribution  

Ignoring layer roles leads to  
**simultaneous delay and DRC failure.**

---

## Routing and DRC

Most routing-related DRCs are:

- Spacing violations  
- Via enclosure violations  
- Antenna violations  

These almost always mean:

> **The router was forced beyond physical limits.**

---

## What Antenna Violations Really Mean

Antenna issues come from:

- Long floating wires
- Charge accumulation during fabrication

Aggressive routing  
**guarantees antenna violations.**

---

## Characteristics of Good Routing

Healthy routing looks like:

- Clear layer separation  
- Minimal vias  
- Straightforward paths  
- Distributed congestion  

You can recognize it instantly in GDS.

---

## Characteristics of Bad Routing

- Serpentine wiring  
- Excessive vias  
- Localized congestion  
- Frequent layer hopping  

👉  
**Magic / KLayout reveal this immediately.**

---

## Practical Completion Criteria

Routing can be considered complete only if:

- Global congestion is acceptable  
- STA does not degrade  
- DRC converges  
- No need to return to floorplan  

If not,  
**routing is not complete.**

---

## Chapter Conclusion

- Routing is not a late-stage task  
- Congestion is the primary enemy  
- Routing problems signal upstream mistakes  
- Returning to floorplan is often the correct decision  

---

## Next Chapter

Next is the most critical bridge between logic and physics.

👉 **`16_GLS_and_SDF.md` — Gate-Level Simulation with Real Delays**

---
