# Adversarial Verification: The Four-Gate Protocol

**Why this protocol exists, how it works, and why it cannot be skipped.**

---

## Why This Exists

Without explicit counter-narrative searching, AI systems will naturally analyze contested situations from whatever perspective is most available. The result is analysis that is coherent, well-sourced from one side, and dangerously incomplete — exactly the kind of unfair, incomplete analysis a civic reporting system is designed to prevent.

To prevent one-sided analysis from ever being produced as intelligence, the adversarial verification protocol was built as a mandatory architectural gate. It forces the system to actively hunt for the other side's response before any contested signal can be finalized. It is a mandatory gate in the Dark Signal Desk that cannot be bypassed.

---

## When It Triggers

The protocol activates whenever a signal involves ANY of the following:

- Accusations against a person or organization
- Claims of wrongdoing, fabrication, or misconduct
- Conflicting accounts of the same event
- Criticism that could materially harm someone's reputation
- Reliance on one party's characterization of events

If any of these apply, adversarial verification is mandatory before the signal can be finalized.

---

## The Four Gates

### Gate 1: Contestation Check

Five yes/no questions. If ANY answer is yes, proceed to Gate 2.

1. Does this signal involve accusations against a person/organization?
2. Does this signal involve claims of wrongdoing, fabrication, or misconduct?
3. Does this signal present conflicting accounts of the same event?
4. Does this signal include criticism that could materially harm reputation?
5. Does this signal rely primarily on one party's characterization?

If all answers are no: document "No contestation detected" and proceed to finalize.

### Gate 2: Mandatory Adversarial Search

Execute ALL four search types. Document every search, including failed ones.

**1. Direct Response Search**
Query: `[accused party name] response to [accusation]`

**2. Official Channel Search**
Query: `site:[accused party website] [topic]`
Query: `site:[accused party social media] [topic]`
If the party has a Reddit presence: `site:reddit.com [party name] [topic]`

**3. Statement Search**
Query: `[accused party name] statement [topic]`

**4. Alternative Framing Search**
Search for the same event using neutral or opposing framing

**Iteration requirement:** If first searches return nothing, try at least 2 variations with different word choices, date ranges, or platforms. Document all attempts.

### Gate 3: Documentation & Synthesis

Document everything in the signal output:

- List every search query executed and its result
- If counter-narrative found: update the structural analysis to present BOTH sides without picking one
- If no counter-narrative found after thorough search: document explicitly ("Extensive search for [party]'s response yielded no results. Searches attempted: [list].")
- If searches failed or were incomplete: flag the signal as INCOMPLETE — do not finalize

### Gate 4: Self-Referential Warning

Extra check for signals about AI, journalism, information integrity, or civic intelligence — topics where the system analyzing the signal may have cognitive blind spots.

If the signal involves criticism of systems similar to what the AI is, apply heightened scrutiny. The system is most likely to rationalize away from uncomfortable findings when analyzing mirrors of its own function.

---

## After All Four Gates

Finalization checklist:
- Phase 1 complete (observation, structural truth, sources)
- Gate 1 complete (contestation check documented)
- Gate 2 complete (all adversarial searches executed and documented)
- Gate 3 complete (synthesis includes counter-narrative or explicit "not found")
- Gate 4 applied if self-referential

**If any item is unchecked, the signal is INCOMPLETE and cannot be published.**

---

## Why You Can't Skip This

The instinct to skip adversarial verification is strongest when the signal feels obviously true. "Of course they did this" or "everyone knows this is wrong" are feelings, not evidence. One-sided narratives that feel right are the most dangerous kind — they pass every other quality check because they're coherent and well-sourced from one perspective.

The adversarial protocol doesn't require you to agree with the counter-narrative. It requires you to find it, document it, and present it. The reader decides who's right. Your job is to make sure they have both sides.

---

## The Design Principle

This protocol embodies the system's core architecture: **fail-open for collection, fail-closed for publication.**

The Black Desk (Prompt 3) collects signals without adversarial checking — speculation is welcome there. But the moment a signal moves toward the Dark Signal Desk (Prompt 4) and approaches anything that could be published, the adversarial gates close. Pass them or get suppressed.

Competing truth claims are more valuable than resolved narratives. If two parties disagree about what happened, that disagreement IS the story. Resolving it prematurely by picking a side is the failure mode this protocol prevents.
