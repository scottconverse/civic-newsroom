# Civic Newsroom — QA Stress Test Report

**Test Date:** March 12, 2026
**Test Operator:** Claude (Anthropic), commissioned by project owner
**Test Prompt Source:** ChatGPT-generated adversarial QA prompt (provided by owner for independence)
**Scope:** All 9 prompts + 5 templates + 1 example sources registry
**Method:** 6-phase audit per the test prompt specification

---

## PHASE 1: SYSTEM INVENTORY

### 1.1 Prompt Catalog

| # | Name | File | Word Count (approx.) | Purpose |
|---|------|------|---------------------|---------|
| 01 | Daily Civic News Aggregator | `prompts/01-news-aggregator.md` | ~2,800 | Ingest civic data, produce 15-25 story leads with tier classification |
| 02 | Story Expansion & Publication | `prompts/02-story-expansion.md` | ~2,600 | Select top leads, expand to 400-800 word stories, enforce Civic Grounding Gate |
| 03 | Black Desk — Speculative Signal Radar | `prompts/03-black-desk.md` | ~1,600 | Stage 0: detect unverified signals from noise (Tier C), cap confidence at 0.5 |
| 04 | Dark Signal Desk — Verification | `prompts/04-dark-signal-desk.md` | ~1,900 | Mandatory 4-gate adversarial verification of escalated signals |
| 05 | News Integrity Checker | `prompts/05-integrity-checker.md` | ~1,300 | Post-production 5-part audit (links, claims, tiers, voices, completeness) |
| 06 | First Amendment Counsel | `prompts/06-first-amendment-counsel.md` | ~1,000 | Legal guidance agent for press freedom, SLAPP, defamation, public records |
| 07 | Plain-Language Translator | `prompts/07-plain-language-translator.md` | ~550 | Rewrite civic reporting at 8th-grade level, preserve facts |
| 08 | Civic Grounding Protocol | `prompts/08-civic-grounding.md` | ~950 | Anti-plagiarism safeguards — journalism as leads only, Hard-No-Bluff Rule |
| 09 | Story Research & Writing Engine | `prompts/09-story-research-writing.md` | ~900 | Standalone 5-stage research + inverted pyramid writing with verification |

### 1.2 Supporting Templates

| Template | File | Purpose |
|----------|------|---------|
| Source Tier Reference | `templates/source-tier-reference.md` | Shared Tier A/B/C/D definitions referenced by all prompts |
| Canonical Sources Registry | `templates/canonical-sources-registry.md` | Blank registry template with tier columns and rejection tracking |
| Story Lead Template | `templates/story-lead-template.md` | Standard lead format for Prompt 01 output |
| Suppression Ledger | `templates/suppression-ledger.md` | Format for documenting killed stories with revision pathway |
| Civic Calendar | `templates/civic-calendar.md` | Meeting schedule template with aggregation timing guidance |

### 1.3 Example Configuration

| File | Purpose |
|------|---------|
| `examples/longmont-colorado/sources-registry.md` | Populated sources registry for Longmont, CO (15 active sources, includes YouTube channel) |

### 1.4 Dependency Map

```
                    ┌──────────────┐
                    │  Prompt 03   │
                    │  Black Desk  │  (Stage 0 — speculation)
                    └──────┬───────┘
                           │ escalates signals
                           ▼
                    ┌──────────────┐
                    │  Prompt 04   │
                    │  Dark Signal │  (verification gate)
                    └──────┬───────┘
                           │ verified signals merge into
                           ▼
                    ┌──────────────┐     ┌──────────────────────┐
                    │  Prompt 01   │◄────│ templates/            │
                    │  Aggregator  │     │ source-tier-reference │
                    └──────┬───────┘     │ canonical-sources-reg │
                           │             │ story-lead-template   │
                           │ leads       │ civic-calendar        │
                           ▼             └──────────────────────┘
                    ┌──────────────┐
                    │  Prompt 02   │◄──── Prompt 08 (Civic Grounding
                    │  Expansion   │      Protocol — enforcement gate)
                    └──────┬───────┘
                           │ stories
                           ▼
                    ┌──────────────┐
                    │  Prompt 05   │◄──── Prompt 08 (independent
                    │  Integrity   │      re-verification)
                    └──────┬───────┘
                           │ approved stories
                    ┌──────┴───────┐
                    ▼              ▼
              ┌──────────┐  ┌──────────┐
              │ Prompt 06│  │ Prompt 07│
              │ 1A Legal │  │ Plain    │
              │ (on-call)│  │ Language │
              └──────────┘  └──────────┘

        Prompt 09 (Research & Writing) = standalone parallel path
        Prompt 08 (Civic Grounding)    = protocol enforced IN Prompts 02 & 05
```

### 1.5 Canonical Execution Order

**Primary pipeline:** 03 → 04 → 01 → 02 (with 08 embedded) → 05 (with 08 embedded) → 07

**On-demand agents:**
- Prompt 06: Triggered by legal threats, not part of regular pipeline
- Prompt 09: Standalone research tool, used outside the pipeline for ad-hoc stories

**Cross-cutting protocol:**
- Prompt 08: Not executed independently — its rules are enforced as gates within Prompts 02 and 05

### 1.6 Ambiguities Identified in Inventory

1. **Prompt 09's relationship to the pipeline is undefined.** It duplicates some of Prompt 01 + 02's functionality (research, writing, verification). No guidance on when to use 09 vs. the 01→02 pipeline.

2. **Prompt 06 has no trigger protocol.** Unlike other prompts, nothing in the pipeline says "if X happens, invoke Prompt 06." It exists but has no on-ramp.

3. **Templates have no version numbers.** The source-tier-reference is referenced by 5+ prompts. If it changes, there's no way to know which prompt version it was last tested against.

---

## PHASE 2: BASELINE EXECUTION TEST (Dry-Run Each Prompt)

For each prompt, I simulate execution mentally using the Longmont, CO configuration and assess whether the instructions produce coherent, complete output.

### Prompt 01: News Aggregator

**Dry-Run Result: PASS**

Step-by-step execution:
1. Part 1 → Check PrimeGov portal → If blocked (robots.txt, JavaScript rendering), skip logic correctly triggers "Packet review deferred" fallback.
2. Part 2 → Multi-source scan of 6 sources → Each source type has clear instructions.
3. Part 3 → Lead compilation uses the story-lead-template format → SOURCE TIER CLASSIFICATION is now mandatory with Tier A/B/C labels → PRIMARY SOURCE GROUNDING STATUS checkbox is a new addition that correctly gates ungrounded leads.
4. Part 9 → Source Discovery Module runs with validation checklist (5/7 threshold).

**Issue found during dry-run:** The Source Tier Classification in Part 3 now includes a long parenthetical defining Tier A (lines 174-181). This works well for Claude/ChatGPT with large context windows but could overwhelm a user copy-pasting into a smaller-context model. The inline definition runs 8 lines. Not a defect — a portability consideration.

### Prompt 02: Story Expansion

**Dry-Run Result: PASS**

Step-by-step execution:
1. Part 1 → Lead selection with >= 0.75 confidence threshold + Pre-Expansion Gate (contact reachable OR source accessible).
2. **Civic Grounding Gate** → Claim-by-claim source tier table → Binary gate decision → 4-question self-check. This is the strongest structural improvement since the first test. It enforces Prompt 08 at the expansion stage with no bypass option.
3. Part 2 → Inverted pyramid structure, 400-800 words.
4. Part 3 → Attribution with JOURNALISM CREDIT format. The example is concrete and correct.
5. Part 4 → 6-step glitch check.
6. Part 6 → Suppression Ledger with revision pathway and DEVELOPING SIGNAL category.
7. Part 7 → Delivery format now includes PRIMARY SOURCE and LEAD SOURCE fields.

**Issue found during dry-run:** The Civic Grounding Gate (lines 67-136) is 70 lines of dense protocol. A user executing this for the first time in ChatGPT would need to carefully track each claim through the table. The gate works, but it demands discipline. If a user skips the table and goes straight to writing, the gate has no external enforcement mechanism.

### Prompt 03: Black Desk

**Dry-Run Result: PASS**

Execution produces signals in the correct format. Cluster definition (3+ reports in 7 days) is now specified. Scan instructions for Phase 1 are concrete. Strength calibration table is clear. The comparison table with Dark Signal Desk (lines 38-46) prevents role confusion.

**No new issues found.**

### Prompt 04: Dark Signal Desk

**Dry-Run Result: PASS**

The 4-gate protocol executes cleanly. Search scope requirements now specify: 3 platforms minimum, 90-day window, 3 query variations. The worked example (utility portal outage, lines 228-256) demonstrates all 6 meta-cognitive steps.

**No new issues found.**

### Prompt 05: News Integrity Checker

**Dry-Run Result: PASS**

The 5-part audit (Links, Claims, Source Tiers, Voices, Completeness) is comprehensive. Part 5 (Source Tier Audit) is a new independent re-verification of Prompt 08 compliance. The publication-readiness threshold (lines 172-187) now has explicit criteria:
- HOLD if UNGROUNDED (overrides all other criteria — correctly stated)
- HOLD if >30% flags or any CRITICAL flag on a core assertion
- PUBLISH WITH CORRECTIONS if GROUNDED/PARTIALLY GROUNDED with only minor flags

FLAG severity is split into CRITICAL vs. MINOR (lines 39-44). This was a previous gap, now closed.

**Issue found during dry-run:** The "did not respond" verification (lines 66-68) requires 2 documented contact attempts. This is a solid standard for human reporters, but AI-generated stories typically can't verify that outreach was attempted — the AI didn't make the calls. This check is more relevant for human QA than AI pipeline verification.

### Prompt 06: First Amendment Counsel

**Dry-Run Result: PASS**

Triage Mode classifies threat severity correctly. Legal analysis format (IRAC-style) is standard. Scope disclaimer is prominent. "Actual malice" now includes a plain-language parenthetical (lines 38-40).

**No new issues found.**

### Prompt 07: Plain-Language Translator

**Dry-Run Result: PASS**

4-part output (Summary, Facts, Interpretations, Impact) is clean. Jargon replacement examples are practical. Section 4 now includes guidance on explaining what happens if a policy condition fails (lines 48-51). Technical term handling (define on first use, then use naturally) is correctly specified.

**No new issues found.**

### Prompt 08: Civic Grounding Protocol

**Dry-Run Result: PASS**

Core rules are clear and absolute. The BAD/GOOD/BETTER examples (lines 47-61) are the most effective teaching tool in the prompt suite. Hard-No-Bluff Rule leaves exactly two options. Self-check has 4 questions with binary pass/fail. Revision pathway exists.

Primary source clarifications (lines 73-79) now cover press releases, audio/video, and public meeting quotes — all previously flagged as ambiguous, now resolved.

**No new issues found.**

### Prompt 09: Story Research & Writing

**Dry-Run Result: PASS**

5-stage research sequence is comprehensive. Source hierarchy is correctly ordered. Attribution templates (lines 88-93) are now included. Gap identification has iteration limits by mode (lines 47-52). Conflicting sources guidance (lines 96-101) includes a concrete example. Headline guidance addresses uncertainty (lines 71-72).

**Minor note:** Prompt 09 does not reference Prompt 08 (Civic Grounding Protocol). A user running Prompt 09 standalone could write a story entirely from journalism sources without any grounding check. This is the only prompt in the suite that produces publishable text without a Civic Grounding gate.

---

## PHASE 3: HUMAN-USE SIMULATION

Testing whether a non-technical user can copy-paste these prompts into ChatGPT, Claude, or Gemini and get usable results.

### 3.1 Portability Assessment

| Factor | Assessment |
|--------|-----------|
| Self-contained instructions | MOSTLY YES — each prompt includes its own role, objective, output format. Exception: Prompt 08 is enforced through other prompts, not run independently. |
| Variable replacement | CLEAR — all `[BRACKETED]` variables are obvious and consistently formatted. |
| Template references | PARTIAL ISSUE — Prompts reference `templates/source-tier-reference.md` but a user copy-pasting a single prompt won't have the template. The critical Tier A definition IS repeated inline in Prompts 01, 02, 03, and 05, mitigating this. |
| Context window fit | PASS for most models — longest prompt (01) is ~2,800 words. All prompts fit within 8K-token context windows. |
| Output format compliance | HIGH — output formats are explicitly defined with field-level templates. AI models follow these reliably. |
| Cross-prompt data handoff | MANUAL — users must copy-paste output from Prompt 01 into Prompt 02, etc. This is expected for copy-paste use but creates friction. |

### 3.2 Common User Failure Points

1. **Forgetting to replace variables.** The prompts have ~15 unique bracketed variables. A user who misses `[YOUR_CITY_AGENDA_PORTAL_URL]` will get generic output. Mitigation: QUICKSTART.md and SETUP-GUIDE.md exist for onboarding.

2. **Running Prompt 02 without Prompt 01 output.** Prompt 02 opens with "Take the 15-25 story leads generated by the Daily Aggregation Prompt." If a user runs 02 standalone without leads, the AI will hallucinate leads. Mitigation: The header says "INPUT: Story leads from Daily Aggregation Prompt" — but a user might ignore this.

3. **Skipping the Civic Grounding Gate.** The gate in Prompt 02 is 70 lines and requires building a claim-by-claim table. A user in a hurry might scroll past it. The AI executing the prompt should still enforce it, but if the user is running in a chatbot that truncates long prompts, the gate could be lost.

4. **Prompt 09 used without Prompt 08 awareness.** As noted above, Prompt 09 has no grounding protocol. A user treating it as the only prompt they need could produce journalism-sourced stories.

### 3.3 Platform-Specific Notes

- **ChatGPT (GPT-4/4o):** Will follow the prompts well. May require "continue" for long outputs from Prompt 01 (15-25 leads) or Prompt 02 (multiple stories). Web browsing mode needed for live source checking.
- **Claude:** Handles long structured prompts natively. Web search available. Will follow grounding gates if the full prompt is included.
- **Gemini:** Will follow format but may be less strict about suppression — could "soften" suppressions into "needs review" language. Gate enforcement less reliable.
- **Smaller models (Llama, Mistral local):** May struggle with the Civic Grounding Gate table and multi-step glitch checks. Prompt 02 is the most demanding prompt for smaller models.

---

## PHASE 4: FAILURE ANALYSIS

### 4.1 Contradictions Between Prompts

**Finding 4.1.1: Confidence scale is now harmonized — previous contradiction resolved.**
Prompt 02 (lines 291-306) includes an explicit conversion table mapping Prompt 01's 0.0-1.0 scale to Prompt 02's 1-10 scale. This was a prior test finding and has been fixed. CONFIRMED RESOLVED.

**Finding 4.1.2: Tier A definition varies slightly across prompts.**
- Prompt 01 (line 174): Defines Tier A inline with YouTube transcripts included.
- Prompt 02 (lines 89-96): Defines Tier A with YouTube and explicitly mentions "official municipal YouTube channel."
- Prompt 05 (lines 105-112): Defines Tier A similarly.
- `source-tier-reference.md`: Full canonical definition.

The definitions are *consistent* but not *identical* in wording. Each prompt includes a parenthetical "See templates/source-tier-reference.md for full definitions." This is acceptable — the canonical definition lives in one place and prompts include summaries. **NOT A CONTRADICTION — acceptable redundancy.**

**Finding 4.1.3: Prompt 09 contradicts the system's grounding philosophy.**
The rest of the pipeline enforces Tier A sourcing through gates in Prompts 01, 02, 05, and the protocol in 08. Prompt 09 has a source hierarchy (lines 56-64) that correctly prioritizes primary documents, but it lacks any enforcement gate. A story produced by Prompt 09 has no Civic Grounding check.

**Severity: MEDIUM.** Prompt 09 is positioned as standalone, so users may not know about Prompt 08. Recommendation in Phase 5.

### 4.2 Gaps in the Pipeline

**Gap 4.2.1: No prompt covers editorial judgment on story selection priority.**
Prompt 01 produces 15-25 leads. Prompt 02 selects 3-6. The selection criteria (confidence >= 0.75, multiple sources, impact) are mechanical. No prompt addresses editorial judgment: "Is this the most important story for our readers today?" The system optimizes for verifiability, not newsworthiness.

**Severity: LOW.** This is by design — the system prioritizes accuracy over editorial discretion, which is appropriate for AI-generated civic news. A human editor would apply this judgment.

**Gap 4.2.2: No prompt handles corrections or retractions.**
If a published story is later found to contain an error, no prompt defines how to issue a correction or retraction. The Suppression Ledger handles pre-publication kills but not post-publication errors.

**Severity: MEDIUM.** Real newsrooms need a corrections policy. This should be documented.

**Gap 4.2.3: No prompt handles multimedia (photos, charts, maps).**
All prompts produce text only. Civic stories about development projects, infrastructure, or boundary changes benefit from maps and visuals. No prompt addresses visual assets.

**Severity: LOW.** Text-first is appropriate for AI civic news. Visual generation is a separate capability.

**Gap 4.2.4: No workflow for recurring/serial coverage.**
If a story (like a multi-meeting rezoning process) spans weeks, no prompt tracks continuity between runs. Each aggregation run starts fresh. The DEVELOPING SIGNAL category in Prompt 02 partially addresses this but only for Dark Signal Desk stories.

**Severity: LOW-MEDIUM.** The Suppression Ledger's "Reopen Trigger" field partially mitigates this.

### 4.3 Edge Cases

**Edge 4.3.1: What happens when ALL leads fail the Civic Grounding Gate?**
Prompt 02 says "A package of 2 fully grounded stories is better than 6 with grounding failures." But what if 0 out of 15 leads have Tier A sources? The prompt doesn't address a day with zero publishable stories.

**Impact:** The system should produce an empty story package with a note: "No stories met publication threshold today. All leads documented in Suppression Ledger." This outcome is not explicitly described.

**Edge 4.3.2: PrimeGov portal is completely inaccessible for weeks.**
The system treats PrimeGov as the primary Tier A source. If it's down for maintenance or redesigned, the pipeline loses its primary grounding mechanism. YouTube transcripts are now a backup, but if the city doesn't post meeting videos promptly either, the pipeline stalls.

**Impact:** The Public Records Request Fallback (Prompt 01, Part 8) exists for this scenario, but CORA requests take 7-10 business days — too slow for daily news.

**Edge 4.3.3: A story is factually correct but structurally mirrors a news article.**
The Civic Grounding self-check asks "Would a journalist recognize their own reporting repackaged?" But what if the AI independently arrived at the same structure because the facts naturally flow that way? The protocol would suppress a correct story.

**Impact:** This is an intentional conservative bias. The system errs on the side of suppression over plagiarism risk. ACCEPTABLE TRADEOFF — noted, not a defect.

### 4.4 Prior Test Findings: Resolution Status

| Prior Finding | Status |
|--------------|--------|
| Confidence scale inconsistency | RESOLVED — conversion table in Prompt 02 |
| Canonical Sources Registry undefined | RESOLVED — template created |
| Cluster sizing undefined (Prompt 03) | RESOLVED — 3+ reports, 7 days |
| Adversarial search scope vague (Prompt 04) | RESOLVED — 3 platforms, 90 days, 3 queries |
| No publication-readiness threshold (Prompt 05) | RESOLVED — explicit criteria added |
| No flag severity weighting (Prompt 05) | RESOLVED — CRITICAL/MINOR split |
| Skip-logic for missing packets (Prompt 01) | RESOLVED — lines 45-49 |
| Suppression Ledger template missing | RESOLVED — template created |
| Source Tier Reference missing | RESOLVED — template created |
| Developing Signal category missing | RESOLVED — added to Prompt 02 |
| Attribution templates missing (Prompt 09) | RESOLVED — 5 templates added |
| Research iteration limits (Prompt 09) | RESOLVED — limits by mode |
| "Actual malice" plain language (Prompt 06) | RESOLVED — parenthetical added |
| Policy consequence explanations (Prompt 07) | RESOLVED — condition failure guidance added |
| Worked example (Prompt 04) | RESOLVED — utility portal example added |

**All 15 prior findings: RESOLVED.** No regressions detected.

---

## PHASE 5: IMPROVEMENT PASS

### Priority 1: Critical (should fix before production use)

**5.1 Add Civic Grounding cross-reference to Prompt 09.**
Prompt 09 is the only prompt that produces publishable text without a grounding gate. Add a section at the end of Prompt 09's Verification Phase:

```
5. CIVIC GROUNDING CHECK: For each factual claim, verify it traces to a
   Tier A source (official government record). If any core claim relies
   solely on journalism reporting (Tier B), either find the primary source
   or convert to headline-only note. See Prompt 08 for full protocol.
```

**Impact:** Closes the only unguarded publication pathway in the system.

**5.2 Add "zero publishable stories" handling to Prompt 02.**
After the TARGET OUTPUT section, add:

```
IF ZERO STORIES PASS THE CIVIC GROUNDING GATE:
Produce a story package with:
- Header showing 0 Publication-Ready Stories
- Complete Suppression Ledger for all attempted stories
- Note: "All leads required primary source verification not available today."
- List of leads with the specific Tier A documents that would unblock them
Do not fabricate stories to fill the package.
```

**5.3 Add corrections/retractions protocol.**
Create a new template `templates/corrections-policy.md` defining:
- When corrections are required (factual error in published story)
- Format for corrections (what was wrong, what is correct, when corrected)
- How to issue retractions (when the entire story is flawed)
- Where to publish corrections (same channel as original story)

### Priority 2: Important (improves quality and robustness)

**5.4 Add journalism credit to Prompt 09.**
Prompt 09 has no equivalent of Prompt 02's JOURNALISM CREDIT format. If a user researches a topic using Prompt 09 and was led to it by a news article, there's no instruction to credit the outlet. Add the same journalism credit format from Prompt 02, Part 3.

**5.5 Standardize Tier A definition wording across all prompts.**
While not contradictory, the varying wording creates maintenance burden. Consider replacing all inline Tier A definitions with a standardized one-liner:

```
(Tier A = official government records. Full definition: templates/source-tier-reference.md)
```

This reduces per-prompt maintenance while preserving the canonical definition.

**5.6 Add version tracking to templates.**
Each template should include a version number and last-modified date. When prompts reference templates, they should note which version they were tested against.

### Priority 3: Nice-to-Have (polish)

**5.7 Add a "pipeline cheat sheet" one-pager.**
A single page showing: which prompt to use when, the canonical execution order, and what each prompt expects as input/output. This aids human users more than AI execution.

**5.8 Add serial coverage tracking guidance.**
Brief section in Prompt 01 or a new template: how to maintain story continuity across multiple aggregation runs for multi-week civic processes (rezoning, budget season, election cycles).

---

## PHASE 6: FINAL REPORT

### Section 1: System Architecture Assessment

The Civic Newsroom is a 9-prompt editorial pipeline with 5 supporting templates, designed for AI-assisted civic reporting. It processes municipal data through a structured sequence: signal detection → aggregation → expansion → verification → translation. The architecture is deliberately conservative — it has more gates and checks than production mechanisms, reflecting a "better to suppress than to publish incorrectly" philosophy.

The strongest architectural feature is the **three-layer grounding enforcement**: Prompt 01 classifies source tiers at ingestion, Prompt 02 enforces a binary grounding gate at expansion, and Prompt 05 independently re-verifies at post-production. Combined with Prompt 08's anti-plagiarism protocol, this creates redundant safeguards against the system's most dangerous failure mode (publishing journalism-sourced content as original reporting).

The weakest architectural point is **Prompt 09's isolation from the grounding protocol**. It is the only prompt that can produce publishable text without a Civic Grounding check.

### Section 2: Prompt-by-Prompt Integrity

| # | Prompt | Structural Integrity | Internal Consistency | Output Clarity |
|---|--------|---------------------|---------------------|----------------|
| 01 | Aggregator | Strong | Clean | High |
| 02 | Expansion | Very Strong | Clean | High |
| 03 | Black Desk | Strong | Clean | High |
| 04 | Dark Signal | Very Strong | Clean | High |
| 05 | Integrity Checker | Very Strong | Clean | High |
| 06 | 1A Counsel | Strong | Clean | High |
| 07 | Translator | Strong | Clean | High |
| 08 | Grounding Protocol | Very Strong | Clean | Very High |
| 09 | Research & Writing | Strong | Clean | High (grounding gap) |

### Section 3: Cross-Prompt Consistency

Tier definitions are consistent across all prompts (with acceptable wording variation). Confidence scales are harmonized through the conversion table in Prompt 02. Suppression Ledger format is shared via template. Source Tier Reference is canonical and properly cross-referenced.

One inconsistency: Prompt 09 does not reference the tier system, grounding protocol, or suppression ledger — it operates as if the rest of the system doesn't exist.

### Section 4: Template Completeness

All 5 templates serve clear purposes:
- **source-tier-reference.md**: Comprehensive, current, includes YouTube. Complete.
- **canonical-sources-registry.md**: Well-structured with tier columns and rejection tracking. Complete.
- **story-lead-template.md**: Matches Prompt 01's output format. Complete.
- **suppression-ledger.md**: Includes revision pathway, reopen triggers, status tracking. Complete.
- **civic-calendar.md**: Clear format with aggregation timing recommendations. Complete.

**Missing template:** Corrections/retractions policy (see Priority 1, item 5.3).

### Section 5: Failure Mode Catalog

| # | Failure Mode | Likelihood | Severity | Mitigation |
|---|-------------|------------|----------|------------|
| F1 | Story published with journalism-only sourcing | Low (post-fix) | Critical | 3-layer grounding enforcement |
| F2 | Prompt 09 produces ungrounded story | Medium | High | No mitigation — gap identified |
| F3 | All leads fail grounding on a given day | Medium | Low | Suppression Ledger captures; no explicit "zero stories" protocol |
| F4 | PrimeGov + YouTube both unavailable | Low | High | CORA fallback (7-10 day delay) |
| F5 | User skips Civic Grounding Gate | Medium (human) | Critical | AI should enforce if prompt is complete |
| F6 | Published story later found incorrect | Low | High | No corrections protocol exists |
| F7 | Signal from Black Desk published without Dark Signal verification | Low | Critical | Pipeline requires 03→04 sequence; no bypass |
| F8 | AI hallucinates a Tier A source URL | Medium | Critical | Integrity Checker link audit should catch |

### Section 6: Scoring on 10 Axes

| Axis | Score (1-10) | Notes |
|------|-------------|-------|
| 1. **Factual Integrity Safeguards** | 9.5 | Best-in-class for AI news systems. 3-layer grounding enforcement. Only gap: Prompt 09. |
| 2. **Anti-Plagiarism Protection** | 9.0 | Hard-No-Bluff Rule + Journalism Credit + self-check questions. Robust. |
| 3. **Source Hierarchy Clarity** | 9.0 | Tier A/B/C/D well-defined. YouTube inclusion is smart. Consistent across prompts. |
| 4. **Structural Completeness** | 8.5 | 9 prompts + 5 templates cover the full pipeline. Missing: corrections policy, Prompt 09 grounding. |
| 5. **Cross-Prompt Consistency** | 8.5 | Confidence scales harmonized. Tier definitions consistent. Prompt 09 is the outlier. |
| 6. **Human Usability (Copy-Paste)** | 8.0 | Clear variables, explicit formats, self-contained instructions. Long gate sections may be skipped. |
| 7. **Platform Portability** | 8.5 | Works on ChatGPT, Claude, Gemini. No platform-specific dependencies. Smaller models may struggle with Prompt 02's gate. |
| 8. **Edge Case Handling** | 7.5 | Handles missing packets, conflicting sources, slow signals. Gaps: zero-story days, serial coverage, corrections. |
| 9. **Adversarial Robustness** | 9.0 | Dark Signal Desk's 4-gate protocol is excellent. Self-referential check (Gate 4) is rare and valuable. |
| 10. **Documentation & Onboarding** | 8.0 | QUICKSTART, SETUP-GUIDE, examples exist. Could use a pipeline cheat sheet. Template versioning missing. |

**Overall Score: 8.55 / 10**

### Section 7: Summary of Findings

The Civic Newsroom prompt system is a mature, well-architected editorial pipeline with robust safeguards against its most dangerous failure modes. All 15 issues identified in the prior test round (March 11) have been resolved. The recent additions — YouTube transcripts as Tier A sources, Civic Grounding Gate in Prompt 02, Source Tier Audit in Prompt 05, and Journalism Credit formatting — significantly strengthen the system.

Three items require attention before production deployment:

1. **Prompt 09 needs a Civic Grounding check** — it's the only unguarded publication pathway.
2. **A corrections/retractions policy is missing** — the system handles pre-publication suppression excellently but has no post-publication error protocol.
3. **Zero-story-day handling should be explicit** — so operators know a blank package is acceptable.

The system's conservative bias (suppress rather than publish) is appropriate for AI-generated civic news and distinguishes it from systems that optimize for content volume.

### Section 8: Comparison to Prior Test

| Dimension | March 11 Test | March 12 Stress Test |
|-----------|--------------|---------------------|
| Open issues found | 15 across all prompts | 3 new (Prompt 09 gap, corrections, zero-story) |
| Prior issues resolved | N/A | 15/15 confirmed resolved |
| Overall score | Not scored | 8.55 / 10 |
| Most improved prompt | N/A | Prompt 02 (Civic Grounding Gate, Journalism Credit) |
| Most improved prompt | N/A | Prompt 05 (Source Tier Audit, publication threshold) |
| System-level improvement | Source tiers inconsistent | Source tiers harmonized with shared reference |

---

## APPENDIX A: File Manifest

```
civic-newsroom/
├── prompts/
│   ├── 01-news-aggregator.md
│   ├── 02-story-expansion.md
│   ├── 03-black-desk.md
│   ├── 04-dark-signal-desk.md
│   ├── 05-integrity-checker.md
│   ├── 06-first-amendment-counsel.md
│   ├── 07-plain-language-translator.md
│   ├── 08-civic-grounding.md
│   └── 09-story-research-writing.md
├── templates/
│   ├── source-tier-reference.md
│   ├── canonical-sources-registry.md
│   ├── story-lead-template.md
│   ├── suppression-ledger.md
│   └── civic-calendar.md
├── examples/
│   └── longmont-colorado/
│       └── sources-registry.md
├── quickstart/
│   ├── QUICKSTART.md
│   └── SETUP-GUIDE.md
└── guides/
    ├── how-to-find-your-sources.md
    ├── how-to-read-a-council-packet.md
    ├── anti-plagiarism-protocol.md
    ├── adversarial-verification.md
    └── filing-public-records-requests.md
```

## APPENDIX B: Recommended Fix Implementation Order

1. Add Civic Grounding cross-reference to Prompt 09 (15 minutes)
2. Add zero-story handling to Prompt 02 (10 minutes)
3. Create corrections-policy.md template (30 minutes)
4. Add journalism credit to Prompt 09 (10 minutes)
5. Add version tracking to templates (15 minutes)
6. Create pipeline cheat sheet (20 minutes)

**Total estimated implementation time: ~2 hours**

---

---

## APPENDIX C: Post-Test Fixes Implemented

The following Priority 1 fixes were implemented immediately after this test:

| Fix | File Modified/Created | Status |
|-----|----------------------|--------|
| 5.1 Civic Grounding check + Journalism Credit added to Prompt 09 | `prompts/09-story-research-writing.md` | DONE |
| 5.2 Zero-story-day handling added to Prompt 02 | `prompts/02-story-expansion.md` | DONE |
| 5.3 Corrections/retractions policy template created | `templates/corrections-policy.md` | DONE |
| 5.4 Journalism Credit added to Prompt 09 | (included in 5.1 above) | DONE |

**Remaining recommendations (Priority 2-3) not yet implemented:**
- 5.5 Standardize Tier A wording across all prompts
- 5.6 Add version tracking to templates
- 5.7 Create pipeline cheat sheet one-pager
- 5.8 Add serial coverage tracking guidance

---

*QA Stress Test completed March 12, 2026. Test prompt provided by project owner via ChatGPT. All 9 prompts and 6 templates audited. Priority 1 fixes implemented same day.*
