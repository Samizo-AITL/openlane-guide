# Contributing Rules — READ BEFORE YOU TOUCH ANYTHING

This repository is **not open for casual contribution**.

It documents a **frozen, battle-tested OpenLane environment strategy**.
Uncontrolled changes defeat its purpose.

If you do not agree with these rules, do not contribute.

---

## Core Rule (Non-Negotiable)

> **Stability beats improvement. Always.**

This repository exists to prevent failure,
not to chase new features, versions, or trends.

---

## What Contributions Are Allowed

You MAY contribute **only if all conditions below are met**:

### ✔ Allowed Contributions

- Clarifying explanations (no behavior change)
- Typo fixes
- Improved wording without altering intent
- Additional failure cases **based on real breakage**
- Documentation of rollback / recovery scenarios
- Notes about what NOT to do

All additions must answer at least one of these questions:

- How does this prevent environment breakage?
- How does this improve reproducibility?
- How does this reduce recovery time?

If not, it does not belong here.

---

## What Contributions Are NOT Allowed

### ❌ Absolutely Forbidden

- “Update to latest OpenLane”
- “Simplify by removing steps”
- “Just run this command instead”
- open_pdks rebuild optimizations
- Conda-based workflows
- Partial setups
- Mixing OpenLane1 and OpenLane2
- Replacing rollback with debugging
- Any change that increases fragility

If your change makes the setup **more flexible**, it is wrong.

---

## Version Policy

- Versions are **intentionally pinned**
- “Outdated” is not a bug
- “Latest” is not a goal

This repository values:
**predictability > novelty**

---

## Pull Request Requirements

All PRs MUST include:

1. **What failure does this prevent?**
2. **What real incident caused this change?**
3. **Why rollback is still the preferred solution**
4. Confirmation that no commands were removed
5. Confirmation that no update paths were introduced

PRs without this information will be closed without discussion.

---

## Language Policy

- English only
- Clear, direct, technical language
- No marketing tone
- No motivational content
- No emojis

This is an engineering survival guide, not a blog.

---

## Philosophy Reminder

- Do not fix → roll back
- Do not update → clone
- Do not rebuild → export/import
- Environment > design

Every contribution must reinforce this philosophy.

---

## Final Statement

This repository is intentionally conservative.

If your instinct is:
> “This could be modernized”

You are in the wrong place.

If your instinct is:
> “This saved me from rebuilding everything”

You are welcome here.
