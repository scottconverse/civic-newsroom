# Post-Update Stress Test Report

**Date:** March 12, 2026
**Scope:** All 9 prompts + 6 templates + 1 cheat sheet + 10 repository docs + 5 guides
**Trigger:** System-wide consistency audit after v2.1 updates (Priority 1-3 fixes + repository doc sync)

---

## Test Methodology

1. Read all 34 markdown files in the repository (9 prompts, 6 templates, 1 cheat sheet, 18 repo/guide files)
2. Automated grep scans for stale references ("5 templates," "three URLs," "v1.0")
3. Cross-reference: every feature mentioned in prompts must appear in relevant docs
4. Cross-reference: every file path referenced must exist
5. Verify Tier A definition consistency across all prompts that define it inline

---

## Phase 1: Prompt Internal Consistency

### Tier A Definition Alignment

All four prompts that define Tier A inline (01, 02, 03, 05) now include:

- YouTube auto-generated transcripts from official municipal channels
- Meeting recordings
- The "when packets aren't posted, check YouTube" fallback
- Reference to `templates/source-tier-reference.md` for full definitions

Prompt 09 uses a shorter definition (lists YouTube transcripts explicitly) and references the canonical doc. **Acceptable — no drift.**

### Cross-Prompt Feature Coverage

| Feature | Prompt(s) | Status |
|---------|-----------|--------|
| Journalism Credit | 02, 09 | Present in both |
| Civic Grounding Gate/Check | 02, 05, 09 | Present in all three publication pathways |
| Zero-story-day handling | 02 | Present |
| Serial Coverage Tracker | 01 (Part 10) | Present |
| Suppression Ledger | 02, 08 | Present with revision pathway |
| Confidence Scale Conversion | 02 (Part 5) | Present |
| Adversarial 4-Gate Protocol | 04 | Present |
| Self-Check (4 questions) | 02, 08 | Present in both |

**Result: PASS — All features present in expected prompts.**

---

## Phase 2: Template & Cheat Sheet Verification

### Template Version Headers

| Template | Version | Tested With |
|----------|---------|-------------|
| source-tier-reference.md | 2.1 | Prompts 01, 02, 03, 05, 09 |
| canonical-sources-registry.md | 2.0 | Prompt 01 Part 9 |
| story-lead-template.md | 2.0 | Prompt 01 |
| suppression-ledger.md | 2.0 | Prompts 02, 05, 08 |
| civic-calendar.md | 2.0 | Prompt 01 |
| corrections-policy.md | 1.0 | QA Stress Test |

**All 6 templates have version headers.** PASS.

### Cheat Sheet Accuracy

| Cheat Sheet Claim | Verified Against | Status |
|-------------------|------------------|--------|
| Pipeline order: 03→04→01→02→05→07 | Prompts | Correct |
| Prompt 08 enforced in 02, 05, 09 | Prompts | Correct |
| 06 = on-demand (legal threats) | Prompt 06 | Correct |
| 09 = on-demand (standalone research) | Prompt 09 | Correct |
| 6 templates listed | templates/ directory | Correct |
| Quick decision tree includes zero-story-day | Prompt 02 | Correct |
| Quick decision tree includes corrections-policy | corrections-policy.md | Correct |

**Result: PASS — Cheat sheet matches current system state.**

### Source Tier Reference — "How Tiers Flow"

**Issue found and fixed:** The "How Tiers Flow" section was missing Prompt 09. Added:
`Research & Writing (Prompt 09) → Built-in Civic Grounding Check; requires Tier A for claims`

**Result: PASS after fix.**

---

## Phase 3: Repository Doc Consistency

### Stale Reference Scan

| Pattern | Files Found | Assessment |
|---------|-------------|------------|
| "5 blank templates" or "five templates" | QA-STRESS-TEST-REPORT.md only | Historical (documents pre-fix state) — ACCEPTABLE |
| "v1.0" | None | PASS |
| "three URLs" or "Find Three Things" | None (only Prompt 03 "three things" = detection postures) | PASS |

### Feature Propagation Across Docs

| Feature | Should Appear In | Actually Appears In | Status |
|---------|-----------------|--------------------|-|
| 6 templates (not 5) | README, QUICKSTART, SETUP, CONTRIBUTING, GitHub Template, LinkedIn, Launch | All 7 | PASS |
| Corrections Policy | README, QUICKSTART, SETUP, CONTRIBUTING, Philosophy, GitHub Template, Launch | All 7 | PASS |
| Pipeline Cheat Sheet | README, QUICKSTART, SETUP, GitHub Template, LinkedIn | All 5 | PASS |
| YouTube as Tier A | README, QUICKSTART, Philosophy, How-to-Find-Sources, Anti-Plagiarism, Launch, LinkedIn | All 7 | PASS |
| Journalism Credit | README, Philosophy, Anti-Plagiarism, Launch, LinkedIn | All 5 | PASS |
| Serial Coverage Tracker | README, QUICKSTART, Philosophy, GitHub Template | All 4 | PASS |
| Prompt 09 Grounding Check | README, Philosophy, Cheat Sheet | All 3 | PASS |
| Zero-story-day handling | Philosophy, Cheat Sheet, GitHub Template | All 3 | PASS |
| "Four URLs" (not three) | QUICKSTART, Launch | Both | PASS |

**Result: PASS — All v2.1 features propagated to all relevant docs.**

---

## Phase 4: Dead Reference Scan

### File Path References

Every `templates/*.md` reference in prompts points to an existing file:

- `templates/source-tier-reference.md` → EXISTS (referenced by 01, 02, 03, 05, 09)
- `templates/suppression-ledger.md` → EXISTS (referenced by 08)
- `templates/canonical-sources-registry.md` → EXISTS (referenced by how-to-find-your-sources)
- `templates/corrections-policy.md` → EXISTS (referenced by QUICKSTART)

### Cross-Prompt References

- Prompt 02 references Prompt 08 → EXISTS
- Prompt 09 references Prompt 08 → EXISTS
- Prompt 05 references Prompt 08 → EXISTS (implicit via "independent check on Prompt 08 compliance")
- Prompt 03 references Prompt 04 (escalation) → EXISTS
- Prompt 01 Part 9 references validation checklist → EXISTS (self-contained)

**Result: PASS — No dead references.**

---

## Phase 5: Contradiction Check

### Checked For

1. **Template count claims vs. actual template count:** 6 everywhere current (except historical QA report) ✓
2. **Tier A definitions across prompts:** Consistent (YouTube included in all) ✓
3. **Pipeline order in cheat sheet vs. actual dependency:** 03→04→01→02→05→07 matches ✓
4. **Prompt 08 enforcement claims:** Cheat sheet says "02, 05, 09" — confirmed in all three ✓
5. **Confidence scale:** 0.0-1.0 in Prompt 01, 1-10 in Prompt 02 with conversion table — no contradiction ✓
6. **Version numbers:** source-tier-reference at 2.1, other templates at 2.0, corrections at 1.0 — consistent with change history ✓

**Result: PASS — No contradictions found.**

---

## Issues Found and Resolved

| # | Issue | Severity | File | Fix |
|---|-------|----------|------|-----|
| 1 | source-tier-reference.md "How Tiers Flow" missing Prompt 09 | Minor | templates/source-tier-reference.md | Added Prompt 09 line |

**Total issues: 1 (minor, fixed during test)**

---

## Overall Assessment

| Dimension | Score | Notes |
|-----------|-------|-------|
| Tier A Consistency | 10/10 | All 5 grounding prompts include YouTube transcripts |
| Template Completeness | 10/10 | All 6 templates have version headers, all referenced |
| Feature Propagation | 10/10 | All v2.1 features appear in all relevant docs |
| Dead References | 10/10 | Every file path and cross-prompt reference resolves |
| Contradiction-Free | 10/10 | No conflicting claims across any files |
| Cheat Sheet Accuracy | 10/10 | Pipeline order, enforcement points, templates all correct |
| Stale References | 9.5/10 | QA report has historical "5 templates" (acceptable) |

**Overall: 9.93/10 — System is internally consistent and publication-ready.**

The one minor issue (Prompt 09 missing from source-tier-reference pipeline flow diagram) was fixed during testing. No other issues found across all 34 files.
