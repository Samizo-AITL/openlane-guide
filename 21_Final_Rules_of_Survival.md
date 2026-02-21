# 21_Final_Rules_of_Survival.md
**The Only Rules That Actually Matter**

---

## Purpose of This Final Chapter

This chapter exists to **end the guide**.

No new tools.  
No new commands.  
No new workflows.

Only the **rules that keep OpenLane alive**.

If you remember nothing else, remember this chapter.

---

## The Fundamental Truth

OpenLane is not fragile.

**Your environment management is.**

Almost every “OpenLane problem” is actually one of the following:

- Version drift
- Environment mutation
- Asset rebuild
- Toolchain mixing
- Unrecoverable updates

These are not bugs.  
They are **self-inflicted wounds**.

---

## Rule 1 — Your Environment Is an Asset

Treat your OpenLane environment as:

- A compiled binary
- A golden image
- A frozen artifact

Not as:

- A playground
- A rolling-release system
- A development sandbox

Once it works, **its value is in staying unchanged**.

---

## Rule 2 — Never Fix a Broken Environment

If something breaks:

❌ Do not debug first  
❌ Do not update packages  
❌ Do not rerun installers  

✔ **Export / import immediately**

Debugging happens **after** preservation, never before.

---

## Rule 3 — Updates Require Cloning, Not Courage

Want to try:

- A new OpenLane version
- A new PDK
- A new Docker version
- A new OS update

The correct process is always:

```
Working environment
        ↓ clone
Experimental environment (allowed to die)
```

Never experiment on your only working system.

---

## Rule 4 — Rebuilding Is Failure

If you hear yourself saying:

- “I’ll just rebuild it”
- “It’s faster to reinstall”
- “I know how to set it up now”

You have already lost.

A reproducible environment is **one that never needs rebuilding**.

---

## Rule 5 — Separation Is Non-Negotiable

These must never touch each other:

- OpenLane1 ↔ OpenLane2
- Production ↔ Evaluation
- Stable ↔ Experimental
- Verified ↔ Unverified

Isolation is not optional.
It is the price of reliability.

---

## Rule 6 — GLS Without SDF Is a Lie

If timing matters:

- STA tells you *where*
- SDF GLS tells you *what actually happens*

Ignoring SDF GLS means accepting functional failure as “mystery”.

Waveforms are not decoration.  
They are evidence.

---

## Rule 7 — If It Ever Worked, It Can Work Again

Once you have:

- A passing `make test`
- A generated GDS
- A clean GLS run

That state is **immortal** as long as you exported it.

Hardware dies.  
OS installs die.  
People make mistakes.

Your environment does not — if you preserved it.

---

## What This Repository Ultimately Teaches

Not OpenLane commands.

Not PDK internals.

Not STA theory.

It teaches **discipline**:

- Discipline to stop changing things
- Discipline to roll back instead of fixing
- Discipline to value stability over novelty

---

## Final Checklist (Memorize This)

- Environment works → **export**
- Something breaks → **import**
- Want changes → **clone**
- Unsure → **do nothing**

This is enough.

---

## Closing Statement

If OpenLane keeps breaking for you,
it is not because OpenLane is unstable.

It is because **you allowed instability in**.

This guide removes that option.

---

**Environment failures are optional.  
You now know how to opt out.**

---
