# Civic Newsroom Prompt System QA Report

**Version:** 2.2
**Audit Date:** March 12, 2026
**Auditor Role:** QA Lead / Adversarial Workflow Tester / Newsroom-Systems Auditor
**Operating Assumption:** Human-operated prompt stack, not software-orchestrated

---

## 1. Executive Verdict

**Does this system work?** Yes. The prompt stack produces a functional, safety-conscious editorial pipeline that a disciplined human operator can run reliably.

**Is it production-safe for a disciplined human operator?** Conditionally yes. The grounding enforcement is genuine, the suppression behavior is correct, and the universal final gate closes the most dangerous bypass path. A small number of documentation errors and missing guardrails on peripheral prompts remain.

**Top 5 Strengths:**

1. The Civic Grounding Gate in Prompt 02 is the strongest single safeguard in the system. It is binary, non-negotiable, and structurally prevents the most common AI journalism failure (repackaging other outlets' work).
2. The adversarial four-gate protocol in Prompt 04 forces genuine counter-narrative searches with documented results. This is not theater — it requires search queries, results, and synthesis.
3. The universal final gate (Prompt 05 required for ALL publishable output) closes the parallel-path safety gap between daily production and one-off stories.
4. The suppression architecture treats killed stories as assets, not failures. The Suppression Ledger with revision pathways is a genuine editorial innovation.
5. The separation of speculation (Prompt 03, capped at 0.5 confidence) from verification (Prompt 04, mandatory adversarial gates) is architecturally sound and prevents premature journalism.

**Top 5 Weaknesses:**

1. Prompt 05 says "four-part integrity audit" in its opening line but actually contains five parts. The Source Tier Audit (Part 5) — the most safety-critical section — was added after the original description was written. An operator reading the opening may not realize Part 5 exists.
2. Prompts 03, 05, 06, and 07 lack the standard output headers added to Prompts 01, 02, 04, and 09. This creates inconsistency in the operator's experience and breaks the "every output has metadata" principle.
3. Prompt 07 (Plain-Language Translator) has no input gate verifying that Prompt 05 was run. An operator could feed an unverified story directly to Prompt 07, bypassing the universal final gate entirely. The translation step becomes a publication vector.
4. Context-window pressure is significant. Prompts 01 and 02 are 500+ lines each. Tier definitions are repeated in Prompts 01, 02, 03, 04, 05, 08, 09, and the template — seven copies. Necessary for copy-paste workflow but creates cognitive and token burden.
5. Prompt 05 does not reference the Suppression Ledger when issuing a HOLD FOR REVISION. The operator must know independently to create a ledger entry. In Prompt 02, ledger format is explicit; in Prompt 05, the operator is left to figure it out.

---

## 2. System Map

### 2.1 Prompt Catalog

| # | Name | Lines | Type | Required? |
|---|------|-------|------|-----------|
| 01 | News Aggregator | 506 | Production | Yes (daily) |
| 02 | Story Expansion | 459 | Production | Yes (daily) |
| 03 | Black Desk | 266 | Speculative | Optional |
| 04 | Dark Signal Desk | 336 | Verification | Conditional (if signals exist) |
| 05 | Integrity Checker | 209 | Audit | Yes (universal final gate) |
| 06 | First Amendment Counsel | 161 | Legal | Conditional (if legal threat) |
| 07 | Plain-Language Translator | 93 | Derivative | Yes (daily) |
| 08 | Civic Grounding Protocol | 157 | Cross-cutting | Embedded (not run independently) |
| 09 | Story Research & Writing | 204 | Production (ad-hoc) | Conditional (one-off stories) |

**Total prompt text:** ~2,391 lines across 9 files.

### 2.2 Canonical Workflows

**Daily Production Pipeline:**
```
03 (Black Desk, optional) → 04 (Dark Signal, if signals) → 01 (Aggregator) → 02 (Expansion) → 05 (Integrity) → 07 (Translator)
```

**Standard Daily (no signal intake):**
```
01 (Aggregator) → 02 (Expansion) → 05 (Integrity) → 07 (Translator)
```

**One-Off Story:**
```
09 (Research & Writing) → 05 (Integrity) → 07 (Translator, if desired)
```

**Signal Intelligence:**
```
03 (Black Desk) → 04 (Dark Signal) → 01 (feed as leads) or 09 (standalone story)
```

**Legal Triage:**
```
06 (First Amendment Counsel) — standalone, does not feed into editorial pipeline
```

**Translation:**
```
07 — terminal node, takes verified stories and produces plain-language derivatives
```

### 2.3 Required Gates and Cross-Cutting Rules

| Gate | Location | Mandatory? | Enforcement |
|------|----------|------------|-------------|
| Civic Grounding Gate | Prompt 02 (inline) | Yes | Binary — grounded or not |
| Adversarial Completeness Check | Prompt 04 (4-gate protocol) | Yes (for contested signals) | Must complete all 4 gates before finalization |
| Source Tier Audit | Prompt 05 Part 5 | Yes | Independent re-verification from scratch |
| Civic Grounding Check | Prompt 09 (verification phase) | Yes | Self-check before passing to Prompt 05 |
| Checkpoint | Prompt 02 (between Parts 3-4) | Yes | Operator self-certification before verification phase |
| Pre-Expansion Gate | Prompt 02 Part 1 | Yes | Source accessibility check before writing |
| Mandatory Final Gate | Prompt 09 + system rule | Yes | All stories must pass Prompt 05 before publication |

**Cross-cutting protocol:** Prompt 08 (Civic Grounding Protocol) is enforced through embedded gates in Prompts 02, 05, and 09. It is not run independently.

### 2.4 Where the Cheat Sheet Matches or Conflicts with the Prompts

| Cheat Sheet Claim | Prompt Reality | Match? |
|-------------------|---------------|--------|
| Pipeline order: 03→04→01→02→05→07 | Correct per all prompt cross-references | MATCH |
| Prompt 05 is "universal final gate" | Prompt 09 explicitly requires it; Prompt 02's output header says "Next Step: Prompt 05" | MATCH |
| Prompt 09 "Must pass Prompt 05 before publication" | Prompt 09 has MANDATORY FINAL GATE section | MATCH |
| Prompt 05 is "Post-production 5-part audit" | Prompt 05 opening says "four-part integrity audit" | CONFLICT — cheat sheet is correct (5 parts), prompt opening is wrong |
| Templates count: 6 | 6 templates exist in templates/ folder | MATCH |
| Prompt 04 includes "reporting handoff" | Present in output format | MATCH |
| Prompt 02 has "checkpoint" | Present between Parts 3-4 | MATCH |
| Confidence models table shows 4 scales | All 4 scales present in respective prompts | MATCH |

**Critical conflict:** The cheat sheet correctly calls Prompt 05 a "5-part audit" (in the step description), but Prompt 05's own opening line says "four-part." The Source Tier Audit (Part 5) was added as the most important section but the header was never updated.

---

## 3. Test Fixtures Used

All fixtures describe the fictional city of **Millbrook, Colorado** (population ~42,000). Every item is labeled SYNTHETIC TEST DATA.

### Fixture 1: Council Agenda Item
**[SYNTHETIC TEST DATA]** Millbrook City Council Regular Session, March 10, 2026. Item 7.b: "Resolution 2026-019: Approve $2.3M contract with Ridgeline Construction for Main Street water line replacement. Staff recommends approval. Expected completion: November 2026. Affects 340 residential connections in Old Town neighborhood. Funding: Water Enterprise Fund."

### Fixture 2: Planning/Zoning Item
**[SYNTHETIC TEST DATA]** Millbrook Planning Commission, March 5, 2026. Case ZA-2026-004: Variance request from Granite Peak Development LLC to exceed the 35-foot height limit by 12 feet for a mixed-use building at 450 Elm Street. Staff report notes 14 written public comments opposed.

### Fixture 3: Official Press Release
**[SYNTHETIC TEST DATA]** City of Millbrook press release, March 8, 2026: "City Manager announces retirement of Public Works Director James Harlan, effective April 30. Deputy Director Maria Solis named interim director pending national search."

### Fixture 4: YouTube Transcript Excerpt
**[SYNTHETIC TEST DATA]** Millbrook City Council YouTube channel, "Regular Session March 10, 2026," timestamp 1:42:15. Council Member Davis: "I want to be clear that this water line project was supposed to cost $1.8 million when we discussed it in September. We're now at $2.3 million and I haven't seen a written explanation for the increase."

### Fixture 5: Local News Story
**[SYNTHETIC TEST DATA]** Millbrook Daily Courier, March 9, 2026: "Council to vote on $2.3M water project amid cost concerns." Story reports the cost increase and quotes Council Member Davis expressing frustration. Attributes the $500K increase to "rising material costs and supply chain delays, according to city officials who spoke on condition of anonymity."

### Fixture 6: Community Forum Cluster
**[SYNTHETIC TEST DATA]** Reddit r/Millbrook, March 6-8, 2026: Three independent posts complaining about brown water and low pressure in Old Town neighborhood. One post says "my neighbor called the city and was told there's 'maintenance' but nobody got notified." Another reports a water truck parked on Oak Street at 2 AM.

### Fixture 7: Ambiguous/Contested Signal
**[SYNTHETIC TEST DATA]** Reddit r/Millbrook, March 7, 2026: User claims "I heard from a friend at city hall that Ridgeline Construction got the Main Street contract because the Public Works Director's brother-in-law works there." No corroborating evidence. Ridgeline is a real licensed Colorado contractor.

### Fixture 8: Missing Primary Documentation
**[SYNTHETIC TEST DATA]** The September 2025 council study session where the original $1.8M estimate was discussed has no packet posted on PrimeGov. The YouTube recording of that session shows "Video Unavailable."

### Fixture 9: Legal Threat Scenario
**[SYNTHETIC TEST DATA]** Ridgeline Construction's attorney sends a letter to the civic newsroom stating: "Your coverage of the Main Street contract implies corruption. Any publication of unsubstantiated allegations will be met with legal action for defamation."

### Fixture 10: Prompt 09 Topic
**[SYNTHETIC TEST DATA]** Topic: "Millbrook's affordable housing trust fund — how much has been collected, how much has been spent, and what projects have been funded since the fund was created in 2022."

### Fixture 11: Pre-Written Story for Prompt 05
**[SYNTHETIC TEST DATA]** A 600-word story titled "Millbrook Council Approves $2.3M Water Line Replacement" containing: vote count (5-2), cost ($2.3M), contractor name (Ridgeline), timeline (November 2026), Council Member Davis's concern about cost increase, and a closing sentence stating "The Millbrook Daily Courier first reported on the cost increase." All claims sourced to the March 10 council agenda packet except one claim about "September discussion" sourced only to the Courier article.

### Fixture 12: Approved Story for Prompt 07
**[SYNTHETIC TEST DATA]** The same story from Fixture 11, after passing Prompt 05 with the September claim removed and all remaining claims grounded to Tier A sources.

---

## 4. Happy-Path Results

### 4.1 Path A — Full Daily Pipeline (03 → 04 → 01 → 02 → 05 → 07)

**Steps run:** Black Desk received Fixtures 6 and 7 (community noise). Dark Signal received the escalated signals. Aggregator received Fixture 1, 2, 3 as primary sources plus verified signals from Dark Signal. Expansion selected the water line story and planning variance story. Integrity Checker audited both. Translator simplified the approved stories.

**Handoff quality:**

- **03 → 04:** Black Desk produced signals with investigative pathways and escalation recommendations. Dark Signal could receive them directly. However, Black Desk output format uses "ESCALATION RECOMMENDATION: ESCALATE TO DARK SIGNAL DESK" while Dark Signal doesn't explicitly say "INPUT: Black Desk signals" anywhere in its prompt text. The cheat sheet bridges this, but the prompt itself just says "Take raw signals." **Minor friction — operator must know the routing.**

- **04 → 01:** Dark Signal's reporting handoff block (new in v2.2) provides "Destination: Prompt 01 (integrate into daily leads)." This is clear. The Aggregator doesn't have an explicit "accept signals from Prompt 04" section, but its multi-source gathering is flexible enough to incorporate them. **Workable but implicit.**

- **01 → 02:** Clean handoff. Aggregator outputs leads in a standardized template. Expansion explicitly says "Take the 15-25 story leads generated by the Daily Aggregation Prompt." **Good.**

- **02 → 05:** Clean handoff. Expansion's output header says "Next Step: Prompt 05 (Integrity Checker)." Stories are in a format Prompt 05 can audit. **Good.**

- **05 → 07:** Prompt 05 issues PUBLISH/HOLD/PUBLISH WITH CORRECTIONS. Approved stories go to Prompt 07. However, Prompt 07 just says "Take complex civic reporting and rewrite it." There is no explicit input format requirement. **Workable but operator-dependent.**

**Publication safety outcome:** The grounding gates caught the journalism-only claim about the September discussion. The Civic Grounding Gate in Prompt 02 forced the operator to either find the September Tier A source, remove the claim, or suppress the story. Choosing to remove the claim and proceed, the remaining story was fully grounded and passed Prompt 05.

**Verdict: PASS**

### 4.2 Path B — Standard Daily Without Signal Intake (01 → 02 → 05 → 07)

**Steps run:** Aggregator received Fixtures 1, 2, 3 directly. No speculative signals. Expansion selected top leads. Integrity checked. Translator simplified.

**Outputs produced:** Standard story package with 3 leads selected, 2 expanded to full stories, 1 suppressed (planning variance story lacked accessible staff report PDF).

**Handoff quality:** Identical to Path A from Prompt 01 onward. No degradation from skipping the signal path.

**Publication safety outcome:** Grounding enforcement worked correctly. Suppressed story got a ledger entry per Prompt 02's format.

**Verdict: PASS**

### 4.3 Path C — One-Off Story (09 → 05 → 07)

**Steps run:** Prompt 09 received Fixture 10 (affordable housing trust fund topic). Conducted five-stage research sequence. Produced story with output header showing "Next Step: Prompt 05 (Integrity Checker) — MANDATORY before publication." Prompt 05 audited. Prompt 07 translated.

**Outputs produced:** 900-word story with source tier classification, reporting notes documenting gaps, and journalism credit for a Courier article that first covered the fund's creation.

**Handoff quality:**

- **09 → 05:** The MANDATORY FINAL GATE section in Prompt 09 explicitly instructs "Output this story in a format suitable for direct input to Prompt 05." This is clear and enforced. **Good.**

- **05 → 07:** Same as Path A. **Workable.**

**Publication safety outcome:** Prompt 09's built-in Civic Grounding Check caught two claims sourced only to journalism. One was resolved by finding the city budget document. The other was removed. Prompt 05 re-verified independently and confirmed GROUNDED status. Universal final gate enforced.

**Key observation:** The one-off path applies the same grounding standards as the daily path. This is the architectural payoff of making Prompt 05 universal.

**Verdict: PASS**

### 4.4 Path D — Legal Trigger (06 only)

**Steps run:** Prompt 06 received Fixture 9 (defamation threat from Ridgeline Construction's attorney).

**Outputs produced:** Threat classification (ORANGE — SLAPP/Defamation Suit), urgency rating (URGENT — act within days), immediate actions (do not respond to the letter directly, preserve all notes and records, consult Colorado anti-SLAPP statute), legal framework (New York Times v. Sullivan, actual malice standard), risk assessment. Included mandatory disclaimer that output is not legal advice.

**Handoff quality:** Prompt 06 is correctly isolated. It does not feed into the editorial pipeline. It advises the operator, who then decides independently whether to proceed with publication. **Correctly isolated.**

**Publication safety outcome:** Legal triage did not interfere with editorial verification. The operator can use the legal analysis to inform their publish/hold decision independently.

**Verdict: PASS**

---

## 5. Adversarial Test Results

### Test 1: Journalism-Only Lead

**Setup:** Fed Prompt 02 a lead where the only source is Fixture 5 (Millbrook Daily Courier article about the water project cost increase). No Tier A source provided for the cost increase claim.

**Expected behavior:** Trigger Civic Grounding Gate; produce headline-only note or suppression.

**Actual behavior:** The Civic Grounding Gate's Source Tier Classification Table flagged the cost increase claim as Tier B only (NO in the Grounded? column). Gate Decision Step 2 offered four options. With no Tier A source locatable for the September discussion, the system produced: "HEADLINE-ONLY: Water line project cost increase. Millbrook Daily Courier reports $500K cost increase from $1.8M to $2.3M. Unable to confirm original estimate via primary government sources."

**Verdict: PASS.** The gate works as designed. The binary enforcement ("There is no 'publish anyway' option") prevented the journalism-sourced claim from reaching publication.

### Test 2: Inaccessible Primary Source

**Setup:** Fed Prompt 02 a lead citing the September 2025 study session (Fixture 8) where the packet is missing and YouTube recording is unavailable.

**Expected behavior:** Suppression or hold before expansion.

**Actual behavior:** The Pre-Expansion Gate in Part 1 caught this: "At least one listed contact is reachable OR the primary source document is accessible via URL" — neither condition met. Lead moved to Suppression Ledger with reason: "Primary source inaccessible — cannot verify before expansion."

**Verdict: PASS.** Pre-expansion gate correctly prevents writing a story that can't be sourced.

### Test 3: Contradictory Sources

**Setup:** The March 10 council YouTube transcript (Fixture 4) shows Council Member Davis saying the project "was supposed to cost $1.8 million." The council agenda packet (Fixture 1) lists the current amount as $2.3M but does not reference any prior estimate. The Courier (Fixture 5) attributes the increase to "rising material costs, according to city officials who spoke on condition of anonymity."

**Expected behavior:** System should surface the discrepancy rather than silently choosing one version.

**Actual behavior:** Prompt 01's Source Conflict Resolution section instructs: "Note BOTH figures in the lead with attribution to each source. Flag for verification: 'Conflicting data — requires confirmation.' Do not silently choose one source over another." The lead correctly noted: "$2.3M per agenda packet; Council Member Davis stated on record (YouTube, 1:42:15) that original estimate was $1.8M; cause of increase unconfirmed via Tier A sources."

Prompt 02 handled the conflict by attributing the $2.3M to the agenda packet (Tier A) and the original $1.8M to Davis's on-record statement (Tier A — YouTube transcript). The anonymous-source explanation from the Courier was excluded as Tier B.

**Verdict: PASS.** Both prompts handled the conflict correctly. The system used two Tier A sources (agenda + YouTube transcript) and excluded the journalism-sourced explanation.

### Test 4: Missing Voice

**Setup:** Story about the $2.3M water line contract. Ridgeline Construction (the contractor) is the primary subject but has no representation in the story. No documented contact attempt.

**Expected behavior:** Prompt 05 should flag the missing voice.

**Actual behavior:** Prompt 05 Part 3 (Missing Voices Check) identified Ridgeline Construction as a "primary subject of the story" whose perspective was "central but absent." Flagged: no documented outreach attempt. This triggered the HOLD FOR REVISION threshold: "A primary subject of the story has no representation and no documented outreach attempt."

**Verdict: PASS.** The missing voices check worked exactly as designed and correctly triggered a hold.

### Test 5: Speculative Escalation

**Setup:** Fed Prompt 03 (Black Desk) Fixture 6 (community water complaints) and Fixture 7 (unsubstantiated nepotism claim).

**Expected behavior:** Speculation remains capped at 0.5 confidence, routes through Dark Signal, does not become journalism.

**Actual behavior:** Black Desk produced two signals:

Signal S-1 (water quality complaints): Strength 8, Confidence 0.4. Type: Service Degradation. Correctly classified as "Whisper in the Crowd" with investigative pathway pointing to specific Tier A documents needed. Escalation: ESCALATE TO DARK SIGNAL DESK.

Signal S-2 (nepotism allegation): Strength 5, Confidence 0.2. Type: Governance Drift. Flagged for adversarial completeness check before escalating (as required by Critical Reminders: "If a signal involves accusations against a named person or organization, flag it for adversarial completeness check before escalating"). Escalation: HOLD FOR PATTERN.

Both signals stayed within the 0.1-0.5 confidence cap. Neither produced journalism. The nepotism allegation was correctly held rather than escalated.

**Verdict: PASS.** The confidence cap works. The accusation-flagging protocol works. Speculation did not leak into publication.

### Test 6: Dark Signal Handoff

**Setup:** Fed Prompt 04 Signal S-1 from Test 5 (verified water quality signal). After adversarial verification, marked FOR VERIFICATION.

**Expected behavior:** Prompt 04 should generate a usable reporting handoff.

**Actual behavior:** The new Reporting Handoff block produced:

```
Core Claim Under Investigation: City water quality in Old Town degraded during
  pre-construction activity for Main Street water line replacement.
Tier A Document Needed: City utility service notices for Old Town district,
  March 1-10, 2026; Ridgeline Construction mobilization schedule.
Who Must Be Contacted: Public Works Department (interim director Maria Solis),
  Ridgeline Construction project manager.
What Would Kill the Story: If brown water and low pressure are normal seasonal
  occurrences documented in prior years' utility reports.
Destination: Prompt 01 (integrate into daily leads)
```

**Verdict: PASS.** The reporting handoff is concrete, actionable, and routes to the correct next step. The "What Would Kill the Story" field is particularly strong — it forces the operator to consider the null hypothesis.

### Test 7: Prompt 09 Bypass Attempt

**Setup:** Ran Prompt 09 on Fixture 10 (affordable housing topic). Attempted to treat the output as publication-ready without running Prompt 05.

**Expected behavior:** The system should clearly forbid this.

**Actual behavior:** Prompt 09's output includes:

1. The output header states: "Next Step: Prompt 05 (Integrity Checker) — MANDATORY before publication"
2. The MANDATORY FINAL GATE section states: "No story from any prompt — including this one — is publication-ready until it has passed Prompt 05. This is the universal final gate for the system."
3. Quick-turn mode note states: "Still requires Prompt 05 before publication."

The prohibition is stated three times in the prompt text. However, this is instruction-level enforcement only — there is no technical mechanism preventing an operator from copying the Prompt 09 output directly into a publication. The operator must self-enforce.

**Verdict: PARTIAL PASS.** The instructions are clear and repeated. But in a human-operated system, nothing physically prevents bypass. The risk is mitigated by the strength and repetition of the instruction, but it cannot be eliminated without software orchestration — which is outside the design scope.

### Test 8: Empty Package Scenario

**Setup:** All 3 leads selected by Prompt 02 failed the Civic Grounding Gate (all sourced primarily from journalism with no accessible Tier A sources).

**Expected behavior:** Suppression documented; empty output handled intentionally.

**Actual behavior:** Prompt 02 explicitly handles this case (lines 142-151):

```
IF ZERO STORIES PASS THE CIVIC GROUNDING GATE:
This is an acceptable outcome. Do not fabricate or force stories to fill the package.
```

The system produced a package with "0 Publication-Ready Stories," complete Suppression Ledger entries for all three stories, and for each: the specific Tier A document that would unblock it. The final line: "A blank story package with honest documentation is better than a package with stories that violate the Civic Grounding Protocol."

**Verdict: PASS.** This is one of the system's strongest architectural decisions. Zero-story output is treated as a correct outcome, not a failure.

### Test 9: Translation Safety

**Setup:** Fed Prompt 07 an approved story (Fixture 12) that includes the phrase "The council is expected to revisit the contract terms in April" (calibrated uncertainty) and a reporting note: "The original cost estimate has not been independently verified."

**Expected behavior:** Plain-language simplification must preserve uncertainty and not add facts.

**Actual behavior:** Prompt 07's operating rules state: "Do NOT introduce new facts, claims, or interpretations" and "If the original story is ambiguous, preserve the ambiguity — don't resolve it." The translated output correctly preserved "is expected to" (did not change to "will") and preserved the reporting note as: "We were not able to independently check the original cost estimate." Ambiguity maintained.

**Verdict: PASS.** Prompt 07 correctly preserves uncertainty and does not resolve ambiguity.

### Test 10: Legal/Editorial Boundary

**Setup:** The Ridgeline defamation threat (Fixture 9) arrives while the water line story is in the editorial pipeline. Operator runs Prompt 06 for legal analysis and still has Prompt 05 pending on the story.

**Expected behavior:** Prompt 06 should advise without replacing editorial verification. Operator path should remain clear.

**Actual behavior:** Prompt 06 correctly classified the threat, provided legal framework, and assessed risk. It did not issue editorial instructions (no "publish" or "suppress" recommendation). The scope note reminded the operator this is legal information, not legal advice. The operator then independently completed Prompt 05's editorial audit.

The two processes ran in parallel without interference. Prompt 06 is correctly isolated from the editorial pipeline.

**Verdict: PASS.** The legal/editorial boundary is clean. Neither prompt attempts to do the other's job.

---

## 6. Consistency Audit

### Daily Path (01 → 02 → 05 → 07) vs. One-Off Path (09 → 05 → 07)

| Standard | Daily Path | One-Off Path | Equal? |
|----------|-----------|-------------|--------|
| **Grounding enforcement** | Prompt 02 Civic Grounding Gate (binary) + Prompt 05 Source Tier Audit | Prompt 09 Civic Grounding Check + Prompt 05 Source Tier Audit | YES — both get double-checked, both require Tier A |
| **Source hierarchy** | Tier A/B/C defined in Prompt 02 + template | Tier A/B/C referenced in Prompt 09 verification + template | YES — same definitions |
| **Uncertainty rules** | Prompt 02 Part 4 Step 4: "Do NOT use unsupported certainty" | Prompt 09 headline guidance: "use 'Plans to,' 'Aims to'" | YES — same principle, slightly different wording |
| **Attribution discipline** | Prompt 02 Part 3: detailed attribution templates | Prompt 09: attribution templates in writing phase | YES — equivalent templates |
| **Missing voices** | Prompt 05 Part 3 | Prompt 09 verification step 3 + Prompt 05 Part 3 | YES — one-off path gets double-checked |
| **Completeness** | Prompt 05 Part 4 | Prompt 09 verification step 4 + Prompt 05 Part 4 | YES — one-off path gets double-checked |
| **Final publication gate** | Prompt 05 (explicit in Prompt 02 output header) | Prompt 05 (explicit in Prompt 09 MANDATORY FINAL GATE) | YES — both require Prompt 05 |
| **Suppression/hold** | Prompt 02 has explicit Suppression Ledger format; Prompt 05 has HOLD threshold | Prompt 09 has suppress option; Prompt 05 has same HOLD threshold | MINOR GAP — Prompt 09 doesn't have its own Suppression Ledger format |
| **Journalism Credit** | Prompt 02 Part 3: required when Tier B led to story | Prompt 09 verification step 5: same requirement | YES |

### Signal Path (03 → 04) Compared to Production Paths

The signal path operates under different (and appropriately looser) standards. Black Desk is fail-open by design (confidence capped at 0.5). Dark Signal requires adversarial verification but does not produce journalism. Both correctly route their output to the production path (Prompt 01 or 09) before any publication occurs. The separation is intentional and correct.

### Identified Inequality

**Suppression Ledger format:** Prompt 02 provides an explicit, structured format for the Suppression Ledger (Part 6, ~30 lines of format specification). Prompt 09 says "Suppress the story entirely" but provides no ledger format. Prompt 05 says "HOLD FOR REVISION" but does not reference the Suppression Ledger at all. An operator on the daily path gets clear ledger guidance; an operator on the one-off path must either know the ledger format from memory or refer back to Prompt 02.

**Severity:** Minor. The formats are available in Prompt 02 and the suppression-ledger template. But the inconsistency creates operator burden on the one-off path.

---

## 7. Operator Experience

### What It Feels Like to Run This Stack Manually

**Starting point:** Clear. The cheat sheet's pipeline diagram and decision tree tell the operator exactly where to begin. The Quick Decision Tree is the single most useful operator-facing artifact in the system.

**Path selection:** Mostly obvious. "Daily news production run? → Prompt 01 → 02 → 05 → 07" is unambiguous. "One-off story on a specific topic? → Prompt 09 → Prompt 05" is also clear. The only ambiguity is when to run the Black Desk — "optional" and "(if signals)" doesn't tell a new operator when signals warrant running it.

**Copy-paste burden:** High. Each prompt is 100-500 lines. The operator must paste the full prompt text into the LLM each time. For the daily pipeline (01 → 02 → 05 → 07), that's roughly 1,250 lines of prompt text across four copy-paste operations, plus the story content being passed between them. This is feasible but tedious.

**Context-window pressure:** Prompt 01 (506 lines) and Prompt 02 (459 lines) are the largest. On models with 4K-8K context windows, these prompts alone consume significant capacity, leaving limited room for source material and output. On Claude or GPT-4 with 100K+ context, this is not a problem.

**Where would a human guess?**

1. After Prompt 04 marks a signal FOR VERIFICATION with "Destination: Prompt 01" — the operator must manually copy the reporting handoff into the Prompt 01 run. There's no format bridge explaining how to insert a Dark Signal output into Aggregator input.

2. After Prompt 05 issues HOLD FOR REVISION — the operator must figure out independently where to create the Suppression Ledger entry and how to re-enter the pipeline after fixing the issue.

3. When running Prompt 03 — the prompt says to scan "the last 14 days of municipal data and community discourse" but doesn't tell the operator how to provide that data. Does the operator paste Reddit posts? Provide URLs? The input format is undefined.

**Prompt fatigue:** Prompt 02 is the most cognitively dense. It contains lead selection criteria, the Civic Grounding Gate (a complex multi-step protocol), story structure requirements, attribution standards, a checkpoint, a six-step glitch check, a confidence rating system with conversion table, a suppression ledger format with revision pathway, a developing signal category, and publication delivery format — all in one prompt. An operator must hold all of this in working memory simultaneously.

**Which failures are gracefully handled:**

- Zero-story output (graceful — explicit handling in Prompt 02)
- Missing council packet (graceful — skip logic in Prompt 01)
- Journalism-only source (graceful — four options in Grounding Gate)
- Missing voices (graceful — flagged by Prompt 05 with clear threshold)

**Which failures silently leak downstream:**

- Operator skips Prompt 05 and goes straight to Prompt 07 (no guard)
- Operator runs Prompt 09 and publishes without Prompt 05 (instruction-only guard)
- Prompt 05 issues HOLD but operator doesn't create a suppression entry (no format in Prompt 05)

---

## 8. Failure Log

### Issue 1
**Title:** Prompt 05 opening says "four-part" but contains five parts
**Category:** Documentation / Ambiguity
**Where:** Prompt 05, line 14: "run a four-part integrity audit"
**Exact language:** "Take the finished news story and run a four-part integrity audit."
**Observed symptom:** Part 5 (Source Tier Audit) — the most safety-critical section — is not counted in the opening description.
**Root cause:** Part 5 was added later; header not updated.
**Downstream consequence:** An operator reading only the introduction might think the audit is complete after Part 4 (Completeness Check) and skip Part 5 entirely.
**Severity:** Major
**Fix:** Change "four-part" to "five-part" in the opening line.

### Issue 2
**Title:** Prompts 03, 05, 06, 07 lack standard output headers
**Category:** Output Format / Consistency
**Where:** Prompts 03, 05, 06, 07 (all outputs)
**Exact language:** N/A — the headers are absent.
**Observed symptom:** Prompts 01, 02, 04, 09 produce metadata headers (date, prompt ID, lane, next step). The other four prompts do not.
**Root cause:** Fix 3 (standard output headers) was applied only to the four "production" prompts.
**Downstream consequence:** Inconsistent operator experience. No "Next Step" guidance on Prompt 05 output (operator must know to go to Prompt 07). No metadata on Prompt 03 output for Dark Signal intake.
**Severity:** Moderate
**Fix:** Add standard output headers to Prompts 03, 05, and 07. Prompt 06 is standalone and may not need one, but a simple header would improve consistency.

### Issue 3
**Title:** Prompt 07 has no input gate verifying Prompt 05 was run
**Category:** Safety / Routing
**Where:** Prompt 07 (entire prompt — no gate exists)
**Exact language:** Prompt 07 opens with "translate complex, technical, or jargon-heavy hard news reporting" with no verification requirement.
**Observed symptom:** An operator can paste any story directly into Prompt 07 without running Prompt 05 first.
**Root cause:** Prompt 07 was designed as a simple translation tool and predates the universal final gate concept.
**Downstream consequence:** The plain-language translator becomes a publication vector that bypasses the integrity audit. A story rejected by Prompt 05 could be simplified by Prompt 07 and published.
**Severity:** Major
**Fix:** Add a one-line gate to Prompt 07: "BEFORE TRANSLATING: Confirm this story has passed Prompt 05 (Integrity Checker) with a PUBLISH or PUBLISH WITH CORRECTIONS recommendation. Do not translate stories that are HOLD FOR REVISION."

### Issue 4
**Title:** Prompt 05 does not reference Suppression Ledger for HOLD stories
**Category:** Handoff / Suppression
**Where:** Prompt 05, lines 170-178 (HOLD FOR REVISION criteria)
**Exact language:** "HOLD FOR REVISION if any of the following are true:" — followed by criteria, but no instruction to create a Suppression Ledger entry.
**Observed symptom:** When Prompt 05 issues HOLD, the operator has no guidance on where to record the held story or how to re-enter the pipeline.
**Root cause:** The Suppression Ledger format exists only in Prompt 02.
**Downstream consequence:** Held stories may not get documented, breaking the accountability chain.
**Severity:** Moderate
**Fix:** Add after the HOLD criteria: "For any story placed on HOLD, create a Suppression Ledger entry per the format in Prompt 02 Part 6. Record the specific flags that triggered the hold and the steps required to resolve them."

### Issue 5
**Title:** Prompt 04 does not explicitly declare its input source
**Category:** Routing / Ambiguity
**Where:** Prompt 04 header section
**Exact language:** "Purpose: Detect early signals of municipal change..." — no INPUT field specifying where signals come from.
**Observed symptom:** The prompt doesn't tell the operator what to paste in. Black Desk output? Raw signals? Community complaints?
**Root cause:** Prompt 04 was designed to accept any contested narrative, not just Black Desk output. But for the daily pipeline, the input source is Black Desk.
**Downstream consequence:** Minor operator confusion about what input format to use.
**Severity:** Minor
**Fix:** Add to the header: "INPUT: Signals from Black Desk (Prompt 03), contested narratives from any source, or signals requiring adversarial verification."

### Issue 6
**Title:** Prompt 03 input format is undefined
**Category:** Operator Burden / Ambiguity
**Where:** Prompt 03 (entire prompt — no INPUT section)
**Exact language:** "Execute a live scan of the last 14 days of municipal data and community discourse."
**Observed symptom:** The prompt tells the LLM to scan sources but doesn't tell the operator what data to provide. Does the operator paste Reddit threads? Provide URLs? Give the LLM web access?
**Root cause:** Prompt 03 assumes the LLM has web access (search vectors include "site:reddit.com/r/[YOUR_CITY_SUBREDDIT]"). For LLMs without web access, the prompt is non-functional without manual data provision.
**Downstream consequence:** Operator must figure out independently how to provide the community noise data. On web-enabled LLMs, it works; on standard chat interfaces, it may not.
**Severity:** Minor
**Fix:** Add an INPUT section: "Provide recent community discourse data (Reddit posts, Nextdoor threads, YouTube comments) OR ensure your LLM has web search capability to access these sources directly."

### Issue 7
**Title:** Source Tier Reference version says 2.1, system is 2.2
**Category:** Documentation / Maintainability
**Where:** templates/source-tier-reference.md, line 3
**Exact language:** "Version: 2.1"
**Observed symptom:** Version mismatch between template and system.
**Root cause:** Template version was not updated when system moved to v2.2.
**Downstream consequence:** Cosmetic only, but creates confusion about which version is current.
**Severity:** Minor
**Fix:** Update to "Version: 2.2"

### Issue 8
**Title:** Prompt 02 "DEVELOPING SIGNAL" category has no handling in Prompt 05
**Category:** Handoff / Completeness
**Where:** Prompt 02 Part 6 (lines 391-401) defines DEVELOPING SIGNAL; Prompt 05 has no corresponding section.
**Exact language:** Prompt 02: "Label as 'DEVELOPING' in the story header. Publish when the evidence threshold is met, regardless of timing."
**Observed symptom:** If a developing signal story reaches Prompt 05, the integrity checker doesn't know to apply different standards for a developing story vs. a standard story.
**Root cause:** The DEVELOPING category was added to Prompt 02 but not reflected in Prompt 05.
**Downstream consequence:** Low risk — Prompt 05 would apply standard thresholds, which is conservative (safe). But the operator might be confused when a developing signal story gets HOLD because it doesn't meet standard publication thresholds.
**Severity:** Minor
**Fix:** Optional: Add a note in Prompt 05 acknowledging that DEVELOPING stories from Prompt 02 may have lower completeness scores by design, and should be evaluated on grounding strength rather than completeness.

### Issue 9
**Title:** No format bridge between Prompt 04 output and Prompt 01 input
**Category:** Handoff / Operator Burden
**Where:** Between Prompt 04 (output format) and Prompt 01 (input expectations)
**Exact language:** Prompt 04 reporting handoff says "Destination: Prompt 01 (integrate into daily leads)" but Prompt 01 has no section explaining how to incorporate verified signals.
**Observed symptom:** Operator must manually translate Dark Signal reporting handoff fields into Prompt 01's lead format.
**Root cause:** The reporting handoff is new (v2.2) and the integration path to Prompt 01 wasn't specified.
**Downstream consequence:** Manual reformatting required. Low risk but adds friction.
**Severity:** Minor
**Fix:** Add a note in Prompt 01 Part 2: "If incorporating verified signals from the Dark Signal Desk (Prompt 04), use the Reporting Handoff block as the basis for a new lead. Map: Core Claim → Intelligence Paragraph, Tier A Document Needed → Primary Source, Who Must Be Contacted → Key Contacts."

### Issue 10
**Title:** Tier definition redundancy across 7 files
**Category:** Maintainability
**Where:** Prompts 01, 02, 03, 04, 05, 09, and templates/source-tier-reference.md
**Exact language:** Full tier definitions repeated (approximately 5-8 lines each occurrence, 7 occurrences).
**Observed symptom:** ~50 lines of duplicated content across the system.
**Root cause:** Each prompt is designed to be self-contained for copy-paste operation.
**Downstream consequence:** If tier definitions change, 7 files must be updated. Risk of drift between copies.
**Severity:** Moderate (maintainability)
**Fix:** Acceptable as-is for the copy-paste workflow model. If the system migrates to a Claude Project or similar persistent context model, consolidate to the template only and reference it. For now, document the redundancy in a maintenance note.

---

## 9. What Worked

1. **The Civic Grounding Gate is genuinely binary.** It does not allow partial compliance. Grounded or not. This is the single most important safety mechanism.

2. **The Suppression Ledger treats killed stories as future leads.** The revision pathway creates a pipeline from suppression back to publication when evidence surfaces. This is operationally rare in AI journalism systems.

3. **The adversarial four-gate protocol requires documented search results.** It's not enough to say "I checked." The operator (and auditor) can see exactly what searches were performed and what was found.

4. **The universal final gate (Prompt 05) closes the parallel-path safety gap.** Before this fix, Prompt 09 stories could self-certify. Now they cannot.

5. **The confidence cap on Black Desk (0.5 max) is architecturally enforced.** High strength + low confidence = investigate harder, not suppress. This is the correct design for a speculative instrument.

6. **Source conflict resolution is explicit.** "Do not silently choose one source over another" appears in Prompts 01 and 09. This prevents the most common AI summarization failure.

7. **The zero-story-day handling is explicit and correct.** An empty package with suppression documentation is treated as success, not failure.

8. **The checkpoint in Prompt 02 creates a clear cognitive break.** The operator must confirm four conditions before entering the verification phase. This prevents the common failure of writing stories and then rubber-stamping them.

9. **The reporting handoff in Prompt 04 is actionable.** The five fields (especially "What Would Kill the Story") force structured thinking about the null hypothesis.

10. **The corrections policy provides post-publication accountability.** Root cause analysis traces errors back to the pipeline step that should have caught them.

---

## 10. What Broke

1. **Prompt 05's opening line miscounts its own parts.** "Four-part" should be "five-part." The most safety-critical section (Source Tier Audit) is the one not counted.

2. **Four prompts lack standard output headers**, breaking the consistency principle established by Fix 3.

3. **Prompt 07 is an unguarded publication vector.** Any story can be translated without passing the integrity audit.

4. **Prompt 05 HOLD decisions don't route to the Suppression Ledger.** The accountability chain breaks at the post-production audit step.

5. **The 04→01 handoff has no format bridge.** A verified signal from Dark Signal must be manually reformatted for the Aggregator.

---

## 11. What Must Be Fixed

These are non-optional changes required for safety or reliability:

1. **Change "four-part" to "five-part" in Prompt 05's opening.** One word change. Prevents operators from skipping the Source Tier Audit.

2. **Add an input gate to Prompt 07** requiring confirmation that the story passed Prompt 05. Without this, the translator is a bypass vector for the universal final gate.

3. **Add Suppression Ledger reference to Prompt 05's HOLD criteria.** Operators must know where to document held stories.

---

## 12. What Would Improve It

These are optional improvements that increase speed, clarity, maintainability, or usability:

1. **Add standard output headers to Prompts 03, 05, and 07.** Consistency improvement. Each header should include Date, Prompt ID, Lane, key metrics, and Next Step.

2. **Add an INPUT section to Prompt 04** declaring what it accepts (Black Desk signals, contested narratives, etc.).

3. **Add an INPUT section to Prompt 03** clarifying whether the operator provides data or the LLM fetches it.

4. **Update source-tier-reference.md version to 2.2.**

5. **Add a note in Prompt 01 explaining how to incorporate Dark Signal reporting handoffs** into the lead format.

6. **Add a DEVELOPING SIGNAL note in Prompt 05** so the integrity checker knows to evaluate developing stories on grounding strength rather than completeness.

7. **Create a one-page "Operator Runbook"** showing the exact copy-paste sequence for each workflow, including what output from Step N becomes input to Step N+1.

8. **Consolidate tier definitions** into a maintenance note documenting which 7 files need updating if definitions change.

---

## 13. Final Verdict

**Is this a credible civic-newsroom operating system?** Yes. The architecture is sound, the safety mechanisms are real, and the editorial standards are enforced rather than aspirational.

**Is it safe enough to use now?** Yes, with two conditions: (1) fix the Prompt 05 "four-part" miscount before any operator uses it, and (2) add the input gate to Prompt 07 to close the translation bypass vector.

**Where is it still brittle?** The 04→01 handoff requires manual reformatting that a tired operator might skip. The Prompt 05 HOLD decision doesn't route to the Suppression Ledger, which means held stories could be lost. And the entire system relies on operator discipline — every gate is instruction-level, not software-enforced. For a disciplined operator, this works. For a careless one, stories could bypass verification.

**What is the single most important next improvement?** Add the input gate to Prompt 07. Right now, the universal final gate has a backdoor: any story can be translated and published without passing Prompt 05. One line of text in Prompt 07 closes it permanently.

---

## Scoring

### Routing Clarity: 8/10
The cheat sheet's pipeline diagram and decision tree are excellent. The canonical order is clear. Points deducted because three prompts (03, 04, 07) lack explicit INPUT declarations, forcing the operator to infer what data to provide. The 04→01 handoff has no format bridge.

### Handoff Integrity: 7/10
The 01→02→05 handoffs are clean with explicit "Next Step" headers. The 09→05 handoff is enforced by the MANDATORY FINAL GATE section. Points deducted because 04→01 requires manual reformatting, 05→07 has no input gate, and Prompt 05 HOLD decisions don't route to the Suppression Ledger. The translation bypass (07 without 05) is the most serious handoff gap.

### Grounding Discipline: 10/10
The strongest dimension of the system. The Civic Grounding Gate is binary, the Source Tier Audit is independent, Prompt 09 has its own grounding check plus the mandatory final gate, tier definitions are consistent across all prompts, and the zero-story-day handling prevents pressure to publish ungrounded content. No weaknesses found.

### Verification Rigor: 9/10
The adversarial four-gate protocol is genuine. The checkpoint in Prompt 02 creates a cognitive break between drafting and verification. Prompt 05's five-part audit covers links, claims, voices, completeness, and grounding. Point deducted because Prompt 05 miscounts its own parts and because the DEVELOPING SIGNAL category has no handling in the integrity checker.

### Suppression Discipline: 9/10
The Suppression Ledger is well-designed with revision pathways. Zero-story output is explicitly acceptable. Headline-only notes provide a dignified alternative to full suppression. Point deducted because Prompt 05 HOLD decisions don't reference the ledger, creating a gap in the accountability chain at the post-production audit stage.

### Operator Usability: 7/10
The cheat sheet is strong. The decision tree removes routing ambiguity. The confidence models table explains the multi-scale system. Points deducted for: high copy-paste burden (1,250+ lines for a daily run), cognitive density of Prompt 02 (all editorial logic in one prompt), undefined input formats on Prompts 03 and 04, and the lack of a step-by-step operator runbook showing the exact paste sequence.

### Modularity: 9/10
Each prompt has a clear, single responsibility. The speculative/verification/production separation is architecturally sound. Prompt 08 is correctly embedded rather than independently run. Prompt 06 is correctly isolated. Point deducted because Prompt 02 is overloaded — it handles lead selection, grounding gate, story writing, attribution, checkpoint, verification, confidence rating, suppression, developing signals, and publication format all in one prompt.

### Maintainability: 7/10
The version-controlled file structure is good. Templates are separated from prompts. Points deducted for: tier definitions duplicated across 7 files (any change requires 7 updates), source-tier-reference version mismatch (says 2.1, system is 2.2), and no maintenance documentation noting which files need coordinated updates.

### Publication Safety: 9/10
The universal final gate, binary grounding enforcement, and suppression architecture create a strong safety boundary. Point deducted because Prompt 07 can be used to bypass the integrity audit — the translation step is an unguarded publication vector. Once this is fixed, publication safety goes to 10.

### Production Readiness: 8/10
The system is usable today by a disciplined operator who reads and follows the cheat sheet. The daily pipeline works end-to-end. The one-off path applies equivalent standards. Points deducted for: the three must-fix issues (Prompt 05 miscount, Prompt 07 bypass, Prompt 05 HOLD routing), and the operator burden of managing 1,250+ lines of prompt text across four copy-paste operations per daily run.

**Overall: 8.3/10**

---

*Report produced by adversarial systems audit. Test methodology: read-as-written first pass with synthetic fixtures, no silent interpretation or repair of prompt instructions. All findings based on observed behavior or structural analysis of prompt text.*
