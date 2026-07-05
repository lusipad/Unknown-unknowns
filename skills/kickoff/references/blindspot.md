# Blind Spot Pass

The user is about to work somewhere they can't see clearly. They may not know what
questions to ask, what good looks like, what historical work exists, or what potholes to
avoid. Explore the territory for them and hand back a map.

**This technique teaches; it never implements.**

## 1. Collect the starting point

Three things (ask once, briefly, only for what's missing): what they're about to do,
what they already know, and what decisions they think they'll face. The gap between what
they think the task involves and what it actually involves is exactly what you're hunting.

## 2. Explore the territory

For codebase work: the modules they'll touch and what those depend on; conventions this
area follows that the rest of the codebase doesn't; history (past attempts, reverted
commits, TODO/FIXME, related PRs); what tests cover and conspicuously don't; hidden
coupling. For domain work: what an expert would consider before starting — vocabulary,
common failure modes, how experts judge quality.

## 3. Deliver the briefing

Exactly these sections, each tight:

1. **The territory** — what this area/domain actually is, in the user's terms
2. **Questions you didn't know to ask** — the heart of the pass; each with why it
   matters and what the answer changes
3. **Potholes** — specific traps, with file references or concrete examples
4. **Prior art** — what already exists that they should reuse or not contradict
5. **What good looks like** — how an expert judges the result; give them a quality bar
6. **Vocabulary** — terms they'll need to prompt precisely

## 4. Help them prompt better

End with **"How to prompt me next"**: their original request rewritten with resolved
assumptions inline and open questions flagged. Decisions only the user can make go to
the interview technique next.
