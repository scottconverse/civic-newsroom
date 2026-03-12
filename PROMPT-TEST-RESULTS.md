# Civic Newsroom Prompt Test Results

**Date:** March 11, 2026
**Test City:** Austin, TX
**Method:** Each prompt was populated with real Austin civic data and run through representative test scenarios.

---

## Results Summary

| # | Prompt | Status | Key Issue |
|---|--------|--------|-----------|
| 01 | Daily Civic News Aggregator | PASS WITH ISSUES | Canonical Sources Registry undefined; circular logic when no packet exists |
| 02 | Story Expansion & Publication | PASS WITH ISSUES | Dual confidence scales (0-1 vs 1-10) create ambiguity across pipeline |
| 03 | Black Desk (Speculative Signal) | PASS WITH ISSUES | Cluster sizing undefined; Tier A document not defined inline |
| 04 | Dark Signal Desk (Verification) | PASS WITH ISSUES | Adversarial search scope vague (platforms? time window? iteration limits?) |
| 05 | News Integrity Checker | PASS WITH ISSUES | No publication-readiness threshold; no flag severity weighting |
| 06 | First Amendment Counsel | PASS | Strong; minor improvement possible on "actual malice" plain-language explanation |
| 07 | Plain-Language Translator | PASS | Clean output; minor gap on explaining policy consequences |
| 08 | Civic Grounding Protocol | PASS | Effective anti-plagiarism safeguards; Suppression Ledger template missing |
| 09 | Story Research & Writing | PASS | Good structure; needs attribution templates and research iteration limits |

**Overall: 0 failures. 6 pass-with-issues. 3 clean passes.**

---

## Prompt 01: Daily Civic News Aggregator

**Status: PASS WITH ISSUES**

### What Worked

- Variable identification is clear and complete; all bracketed fields map to real civic infrastructure (Legistar, CapMetro, AISD, Travis County)
- Lead template (HEADLINE / CATEGORY / CONFIDENCE / CONTACTS / NEXT STEPS) produces scannable, actionable output
- Privacy note (lines 95-100) correctly distinguishes public officials from private citizens
- Confidence scoring system (0.0-1.0 with defined thresholds) is well-calibrated
- Multi-source approach (6 source categories) prevents over-reliance on any single feed

### Issues Found

**1. Circular logic when no agenda packet exists (lines 35-44)**
The prompt says "START with City Council packet analysis" but only adds "if available" parenthetically. Austin's March 12 agenda was listed as "not available" during testing. No decision tree for what to do next.
**Fix:** Add explicit skip-logic: "If no packet posted, proceed to Part 2 sources and flag 'Packet review deferred' in output."

**2. Canonical Sources Registry never defined (Part 9, lines 308-368)**
The source discovery module instructs users to "add to Canonical Sources Registry" with tier recommendations, but the registry itself has no format, location, or template. Users cannot complete Part 9 without external context.
**Fix:** Provide a sample registry template (spreadsheet columns: URL, Last Checked, Frequency, Tier, Notes) and specify where to store it.

**3. Time allocation inflexibility (lines 383-388)**
30 minutes for packet analysis doesn't scale — some Austin packets are 100+ pages. No guidance on when to stop and move on.
**Fix:** "After 20 minutes, move to secondary sources. Mark remaining items as 'deferred to next cycle.'"

**4. Anti-plagiarism protocol referenced but not included (line 134)**
SOURCE 6 references an "anti-plagiarism protocol" — this is defined in Prompt 08, but a user running Prompt 01 alone would not have it.
**Fix:** Add a cross-reference: "See Prompt 08 (Civic Grounding Protocol) for full anti-plagiarism safeguards."

**5. No source hierarchy for conflicting data (Part 5)**
When AISD's website and a news article give different school closure counts, the prompt doesn't specify which source wins.
**Fix:** Add: "Official government sources take priority. When sources conflict, note both and flag for verification."

---

## Prompt 02: Story Expansion & Publication

**Status: PASS WITH ISSUES**

### What Worked

- Lead selection criteria (confidence >= 0.75, multiple sources, specific facts) are clear and enforceable
- Inverted pyramid story structure is well-specified with paragraph-level guidance
- Glitch check (6 steps) is thorough — particularly the "over-certain language" and "inferred causation" checks
- Suppression ledger is a strong accountability mechanism
- Prohibited language list ("Sources say...", "It is believed...", "Some residents think...") catches real pitfalls

### Issues Found

**1. Dual confidence scales create pipeline confusion**
Prompt 01 uses 0.0-1.0 confidence. Prompt 02 introduces a 1-10 rating. A lead arriving at 0.85 from Prompt 01 must be mentally re-mapped to the 1-10 scale. No conversion guidance provided.
**Fix:** Standardize on one scale across all prompts, or add an explicit conversion table.

**2. Contact verification not required before expansion**
The prompt expands leads into 400-800 word stories but doesn't require verifying that listed contacts are reachable first. A story could be "publication-ready" with a disconnected phone number.
**Fix:** Add a pre-expansion gate: "Before expanding a lead, verify at least one contact is reachable or that the primary source document is accessible."

**3. Suppression ledger lacks a "revision pathway" (Part 6)**
Once suppressed, a story has no defined path back to publication. The ledger says "suggest how to make publishable" but doesn't define a re-evaluation workflow.
**Fix:** Add: "Suppressed stories may be re-evaluated after obtaining the missing information. Re-run glitch check before publishing."

---

## Prompt 03: Black Desk (Speculative Signal Radar)

**Status: PASS WITH ISSUES**

### What Worked

- Three detection postures (Dog That Didn't Bark, Whisper in the Crowd, Fiscal Fray) are creative and operationally useful
- Confidence cap at 0.5 explicitly prevents over-confidence in unverified signals — this is well-designed
- Signal output template (ANOMALY > STRUCTURAL PRESSURE > DIVERGENCE > INVESTIGATIVE PATHWAY) bridges speculation to action
- Ethics note on surveillance vs. journalism (lines 236-243) is important and well-placed
- Clear separation from Dark Signal Desk role prevents contamination between speculation and verification

### Issues Found

**1. "Cluster" never defined (lines 100-104)**
The Retaliation Filter asks users to "cluster complaints by timing against known civic controversy events" but never says how many complaints constitute a cluster or within what time window.
**Fix:** Add: "3+ independent reports within 7 days, from different sources or geographic areas, constitutes a reportable cluster."

**2. Strength vs. confidence relationship confusing (lines 196-204)**
A signal with strength 13 (urgent) and confidence 0.2 (very low) may feel contradictory. Line 204 clarifies this, but it's buried.
**Fix:** Move the "High strength + low confidence = strong investigative priority" explanation to the top of the prompt or to a boxed callout.

**3. Tier A document not defined inline (line 172)**
Investigative pathway says "Tier A document required" but Tier A is only defined elsewhere in the prompt suite.
**Fix:** Add quick-reference: "Tier A = official public record on government portal (minutes, budgets, permits, resolutions)."

**4. Phase 1 scan methodology vague (lines 87-91)**
Search vectors list portals but don't specify what to look for (keyword search? manual scan of last 14 days? check for specific withdrawal patterns?).
**Fix:** Add concrete scan instructions: "Search portal for 'withdrawn,' 'tabled,' 'postponed.' Scan consent agendas for items over $50K."

---

## Prompt 04: Dark Signal Desk (Verification Protocol)

**Status: PASS WITH ISSUES**

### What Worked

- Mandatory 4-gate adversarial protocol is the strongest verification framework in the suite
- Gate 4 (self-referential warning) is a rare and valuable feature — checking for blind spots when analyzing systems like itself
- Wide-aperture mandates (lines 176-193) prevent premature filtering of weak signals
- "Routine Is a Cloak" principle (lines 186-189) is insightful and operationally useful
- Signal spectrum (10 categories) provides good taxonomic coverage

### Issues Found

**1. Adversarial search scope undefined**
Gate 2 says to search for counter-narratives but doesn't specify: which platforms to search, how far back in time, how many query variations to try before concluding "not found."
**Fix:** Add: "Search minimum 3 platforms (official website, news, social media). Time window: 90 days. Try at least 3 query variations before documenting 'not found.'"

**2. Tension between "fail-open" and "fail-closed"**
The prompt says "Fail-open collection, fail-closed escalation" but doesn't clearly define the boundary. At what point does an open-collected signal become closed for escalation?
**Fix:** Add a clear escalation threshold: "A signal moves from collection to escalation only after all 4 gates are completed with documented results."

**3. Meta-Cognitive Reasoning Protocol underspecified (lines 212-219)**
The DECOMPOSE/SOLVE/VERIFY/CHECK/SYNTHESIZE/REFLECT steps are listed but not exemplified. A user encountering this for the first time would not know how to execute it.
**Fix:** Add one worked example showing all 6 steps applied to a sample signal.

---

## Prompt 05: News Integrity Checker

**Status: PASS WITH ISSUES**

### What Worked

- 4-part audit structure (Links, Claims, Voices, Completeness) is comprehensive and systematic
- CONFIRMED / FLAG / UNVERIFIED status labels are clear and actionable
- Missing Voices section catches unrepresented stakeholders — this is often overlooked in automated checks
- Standards section (lines 114-122) correctly notes that FLAGS are not suppression recommendations

### Issues Found

**1. No publication-readiness threshold**
The prompt flags issues but never says how many flags = "do not publish." A story with 8 out of 10 claims flagged still has no explicit stop signal.
**Fix:** Add: "If more than 30% of factual claims are FLAGged, or any claim in the lede is UNVERIFIED, recommend holding for revision."

**2. No flag severity weighting**
A wrong job title and a fabricated vote count are both "FLAGS." The prompt doesn't distinguish between minor attribution errors and fundamental factual problems.
**Fix:** Add severity levels: "CRITICAL FLAG (wrong facts, fabricated data) vs. MINOR FLAG (title error, missing middle initial)."

**3. Non-response documentation guidance missing**
The test story included "City Manager's office did not respond to requests for comment." The prompt checks for missing voices but doesn't specify how to verify that outreach was actually attempted.
**Fix:** Add: "For 'did not respond' claims, verify that the reporter can document at least 2 contact attempts with dates."

---

## Prompt 06: First Amendment Counsel

**Status: PASS**

### What Worked

- Triage mode immediately classifies threat severity (RED/ORANGE/YELLOW) with clear escalation
- Correctly identifies Texas anti-SLAPP statute (CPRC Section 27.001) for the Austin test scenario
- Controlling case law cited precisely (Sullivan, Gertz, Milkovich, Branzburg)
- Risk assessment is realistic — no false reassurance
- Scope disclaimer is prominent and correctly positioned
- Immediate actions are in priority order and include "what NOT to do" (don't delete posts, don't call opposing counsel)

### Minor Improvement Opportunities

- "Actual malice" standard could include a one-sentence plain-language definition for non-lawyers
- Could add a "what not to say in the interim" section (don't admit fault, don't discuss with opposing counsel)
- Could add a "quick diagnostic" question upfront: "Are the flagged statements facts or opinions?"

---

## Prompt 07: Plain-Language Translator

**Status: PASS**

### What Worked

- Successfully converts complex civic jargon to accessible language without losing meaning
- "Easement dedication" > "legal right-of-way set aside" demonstrates excellent translation quality
- 4-part output structure (Summary, Facts, Interpretations, Impact) clearly separates layers of information
- Tone guidance ("smart neighbor who doesn't follow city politics") is well-calibrated
- Correctly preserves ambiguity when original reporting is unclear

### Minor Improvement Opportunities

- Could explain consequences of failing conditions (what happens if the revenue neutrality test fails?)
- Transit corridor explanation could briefly note why it matters (future public transportation investment)
- Could flag kept technical terms with inline definitions on first use

---

## Prompt 08: Civic Grounding Protocol

**Status: PASS**

### What Worked

- Core rule (Journalism as LEADS, not SOURCES) is crystal clear and reinforced multiple times
- BAD / GOOD / BETTER attribution examples (lines 47-61) are concrete and prevent subtle plagiarism-by-paraphrase
- Hard-No-Bluff Rule leaves exactly two options (headline-only note or skip) — no wiggle room
- Self-check question 4 ("Would a journalist recognize their own reporting repackaged?") is an excellent gut-check
- "When Journalism Is the Story" exception (lines 102-114) handles edge cases without creating loopholes

### Minor Improvement Opportunities

- Primary source definition could be tightened: Are city press releases primary or secondary? Are audio recordings usable before transcription?
- Suppression Ledger is referenced (line 135) but no template is provided — should include one
- "Exclusive quote" flag (lines 76-77) needs clarification for quotes sourced from public meeting records
- Self-check could add a revision pathway: what if a story fails checks but could be fixed?

---

## Prompt 09: Story Research & Writing Engine

**Status: PASS**

### What Worked

- 5-stage research sequence (Core Event > Stakeholders > Context > Competing Narratives > Gaps) is comprehensive
- Source hierarchy (lines 47-54) is well-defined and correctly prioritizes primary documents
- Writing standards align with AP journalism norms
- Verification phase includes practical link-checking and missing-voices audit
- Mode guidance (Quick-Turn / Standard / Deep Investigation) provides needed flexibility
- "Reporting notes" appendix ensures transparency about gaps

### Minor Improvement Opportunities

- Gap identification (Stage 5) needs iteration limits: how many additional searches before accepting a gap?
- Attribution lacks templates — should include examples of inline attribution formats
- Conflicting source handling is mentioned but not exemplified
- Headline guidance should address uncertainty: use "Plans to" or "Aims to" instead of "Will" for unconfirmed timelines
- Word count threshold for switching modes could be clearer

---

## Cross-Prompt Issues

These affect the system as a whole rather than individual prompts.

**1. Confidence Scale Inconsistency**
Prompts 01, 03, 04 use 0.0-1.0. Prompt 02 uses 1-10. Prompt 05 uses 1-10 but with different thresholds. This creates friction when signals flow through the pipeline (03 > 04 > 01 > 02 > 05).
**Recommendation:** Standardize on one scale system-wide, or add a conversion table to Prompt 02.

**2. Suppression Ledger Referenced in Multiple Prompts but Never Templated**
Prompts 02 and 08 both reference a Suppression Ledger. Neither provides a reusable template.
**Recommendation:** Create a shared Suppression Ledger template and reference it from both prompts.

**3. Tier System Used Inconsistently**
Prompt 03 references Tier A/B/C sources. Prompt 04 references Tier A/B/C with slightly different definitions. Prompt 01's source discovery module adds tier recommendations without defining the baseline.
**Recommendation:** Create a shared Source Tier Reference document that all prompts link to.

**4. Slow Signals Don't Fit Prompt 02's Timing Criteria**
Prompt 04 detects slow-burn signals (administrative drift, fiscal stress). Prompt 02 requires "newsworthy timing (within 1 week)" for strong stories. No pathway exists for slow signals that are important but not timely.
**Recommendation:** Add a "Developing Signal" publication category in Prompt 02 for long-cycle stories.

---

## Recommended Priority Fixes

### High Priority (fix before production use)

1. Standardize confidence scales across all prompts (or add conversion table)
2. Define the Canonical Sources Registry format and location (Prompt 01)
3. Add publication-readiness threshold to Prompt 05
4. Add adversarial search scope parameters to Prompt 04
5. Add skip-logic for missing agenda packets in Prompt 01

### Medium Priority (improve quality)

6. Create shared Suppression Ledger template
7. Create shared Source Tier Reference document
8. Add cluster-sizing guidance to Prompt 03
9. Add attribution templates to Prompt 09
10. Add flag severity weighting to Prompt 05

### Low Priority (polish)

11. Add "actual malice" plain-language definition to Prompt 06
12. Add policy-consequence explanations to Prompt 07
13. Add worked example to Prompt 04's meta-cognitive protocol
14. Clarify primary source definition in Prompt 08
15. Add "Developing Signal" category to Prompt 02
