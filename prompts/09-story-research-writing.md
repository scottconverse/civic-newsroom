# Prompt 9: News Story Research & Writing Engine

**A standalone research and writing agent. Give it a topic and it conducts a structured five-stage research sequence, then writes a publication-ready newspaper story with built-in verification.**

---

```
================================================================================
CIVIC NEWSROOM - NEWS STORY RESEARCH & WRITING
================================================================================

Research and write a newspaper-style news story on the following topic(s):

[TOPIC]

================================================================================
RESEARCH PHASE
================================================================================

Conduct research using web search in a structured sequence:

1. CORE EVENT SEARCH
   Search for the central facts — what happened, when, where, and who is
   directly involved. Prioritize primary sources: government records, official
   agendas and minutes, agency press releases, court filings, public data sets.

2. STAKEHOLDER AND RESPONSE SEARCH
   Identify all relevant parties — officials, agencies, organizations, affected
   residents, advocates — and search for their public statements, positions,
   or actions related to the topic.

3. CONTEXT AND PRECEDENT SEARCH
   Search for historical background, prior coverage, related policy decisions,
   and comparable situations in other jurisdictions that give the reader a
   framework for understanding significance.

4. COMPETING NARRATIVES SEARCH
   Actively search for dissenting viewpoints, criticism, alternative
   interpretations, or opposition to the dominant framing. Do not produce a
   press release rewrite — surface the tension in the story.

5. GAP IDENTIFICATION SEARCH
   Based on what you've gathered, identify what's still missing — unanswered
   questions, unavailable data, parties who haven't made public statements —
   and conduct targeted searches to fill those gaps.

   Iteration limits by mode:
   - Quick-turn: 2-3 targeted gap searches, then document remaining gaps
   - Standard: 3-5 targeted gap searches per major gap
   - Deep investigation: 5+ searches per gap, including cross-jurisdictional
   After reaching the limit, document unfilled gaps in Reporting Notes rather
   than continuing to search indefinitely.

SOURCE HIERARCHY

Rank and weight sources in this order:
1. Primary documents — agendas, ordinances, filings, budgets, permits, records
2. Direct statements from named officials or stakeholders
3. Established news outlets with original reporting
4. Subject-matter experts and institutional analysis
5. Secondary coverage and commentary

When sources conflict, note the discrepancy in the story rather than choosing
one silently.

================================================================================
WRITING PHASE
================================================================================

Headline: Concise, specific, engaging. Active verbs. No clickbait.
When timeline is uncertain or has a history of delays, use "Plans to," "Aims to,"
or "Expects to" rather than "Will" to avoid conveying false certainty.

Subhead (optional): One line that adds a second dimension.

Story structure: Open with a strong lede delivering the most newsworthy element.
Follow with a nut graf establishing why this matters and to whom. Layer in
supporting details, background, and context in descending order of importance.

Standards:
- Factual, neutral tone — no editorializing, no speculative language, no advocacy
- Attribute all information to its source using inline attribution
- Include direct quotes where available, attributed to named individuals
- Prefer specificity — dates, dollar amounts, vote counts, locations, agency names
- When key information is unavailable or unconfirmed, say so transparently
- Where relevant, include contact information and URLs in plain-text format

Attribution Templates:
- Official document: "According to the [document title], [fact]."
- Named official: "[Name], [title] of [organization], said [quote/fact]."
- Government record: "The city's [report/filing/budget] states [fact]."
- Public meeting: "During the [date] [body] meeting, [official] said [quote]."
- When paraphrasing: "The [organization] [verb — announced, reported, filed] that [fact]."

When Sources Conflict:
- Present both versions with attribution: "[Source A] states [X], while [Source B]
  reports [Y]. The discrepancy has not been publicly addressed."
- Do not silently choose one version over the other
- If one source is a primary document and the other is secondary reporting,
  note the source type: "City budget documents show $2.1M, though [outlet]
  reported $2.4M citing unnamed officials."

Target length: 600-1,200 words unless complexity demands more.
Exceed 1,200 words when:
- Multiple competing stakeholder positions each require full explanation
- Historical context is essential to understanding the current event
- Complex policy decisions require detailed breakdown for reader comprehension
- The story spans multiple jurisdictions or intersecting issues
There is no hard ceiling — complexity determines appropriate length.

================================================================================
OUTPUT HEADER (Prepend to story output)
================================================================================

---
Date: [DATE]
Prompt: 09 — Story Research & Writing
Lane: One-Off / Ad-Hoc
Topic: [TOPIC]
Mode: [QUICK-TURN / STANDARD / DEEP INVESTIGATION]
Grounding Status: [GROUNDED / PARTIALLY GROUNDED / UNGROUNDED]
Disclosure: This report was produced using AI-assisted analysis of public government records.
Next Step: Prompt 05 (Integrity Checker) — MANDATORY before publication
---

================================================================================
VERIFICATION PHASE
================================================================================

Before finalizing the story:

1. LINK CHECK: Confirm every URL resolves correctly and points to relevant content.
   Replace or remove broken links.

2. CLAIM AUDIT: Review each factual claim. Flag anything that relies on a single
   unverified source or could not be cross-referenced.

3. MISSING VOICES CHECK: Identify who was not quoted or represented. Note any
   stakeholder whose perspective is absent — particularly anyone directly
   affected. If unavailable, note in the story.

4. COMPLETENESS CHECK: Identify open questions the story doesn't answer. Append
   a brief editorial note:
   "Reporting notes: [description of gaps, pending responses, areas for follow-up]"

5. CIVIC GROUNDING CHECK: For each factual claim in the story, verify it traces
   to a Tier A source — an official government record on a .gov portal, official
   meeting transcript, YouTube auto-generated transcript from the city's official
   channel, budget, permit, resolution, or official press release.
   (See templates/source-tier-reference.md for full tier definitions.)

   If any core factual claim relies solely on journalism reporting (Tier B) and
   cannot be independently verified from a Tier A source:
   → Find the Tier A source now (agenda portal, YouTube transcript, city clerk), OR
   → Remove the ungrounded claim from the story, OR
   → Convert the story to a HEADLINE-ONLY NOTE, OR
   → Suppress the story entirely.

   See Prompt 08 (Civic Grounding Protocol) for full anti-plagiarism safeguards,
   including the Hard-No-Bluff Rule and the 4-question self-check.

   JOURNALISM CREDIT (Required when a Tier B outlet led you to the story):
   If a newspaper, TV station, or news site's reporting identified the topic you
   then independently verified from Tier A sources, credit the outlet:
   "[Paper name] first reported on [topic]" or "[Paper name] coverage provides
   additional context." Place in the closing paragraph — not as a source citation
   for any specific factual claim. This is not optional.

================================================================================
MANDATORY FINAL GATE
================================================================================

BEFORE PUBLISHING any story produced by this prompt, run Prompt 05
(Integrity Checker) as an independent post-production audit.

Prompt 09's built-in verification (steps 1-5 above) is a self-check.
Prompt 05 is an independent audit that re-verifies grounding from scratch,
tests every link, audits every claim, checks for missing voices, and makes
a publish/hold recommendation.

No story from any prompt — including this one — is publication-ready until
it has passed Prompt 05. This is the universal final gate for the system.

Output this story in a format suitable for direct input to Prompt 05.

================================================================================
MODE GUIDANCE
================================================================================

QUICK-TURN (breaking news, single-source):
Prioritize speed. Core event + stakeholder searches. 400–600 words. Flag gaps.
Still requires Prompt 05 before publication.

STANDARD (most topics):
Full five-stage research. 600–1,200 words.

DEEP INVESTIGATION (complex civic, policy, accountability):
Extended research across all stages with additional passes. No word limit.
Pursue document trails and cross-jurisdictional comparisons.

================================================================================
END PROMPT 9
================================================================================
```
