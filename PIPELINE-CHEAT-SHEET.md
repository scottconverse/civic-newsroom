# Civic Newsroom — Pipeline Cheat Sheet

**Version:** 2.2 | **Last Modified:** March 12, 2026

One-page reference for which prompt to use, when, and what it expects.

---

## Primary Pipeline (Daily Run)

```
STEP 1 ──► STEP 2 ──► STEP 3 ──► STEP 4 ──► STEP 5
  03          04          01          02          05 → 07
Black Desk  Dark Signal  Aggregator  Expansion   Integrity → Translation
(optional)  (if signals) (daily)     (daily)     (daily)     (daily)
```

| Step | Prompt | What It Does | Input | Output |
|------|--------|-------------|-------|--------|
| 1 | **03 — Black Desk** | Scans for unverified signals in community noise (Reddit, Nextdoor, YouTube comments). Confidence capped at 0.5. | Last 14 days of civic data + community discourse | Speculative signals with investigative pathways |
| 2 | **04 — Dark Signal** | Runs signals through mandatory 4-gate adversarial verification. Includes reporting handoff for verified signals. Handoff destination: **Prompt 01** (integrate into daily leads) or **Prompt 09** (standalone story). | Black Desk signals (or any contested narrative) | Verified/rejected signals with documentation + reporting handoffs |
| 3 | **01 — Aggregator** | Scans council packets, official sources, and verified signals. Produces 15-25 story leads. | City agenda portal, official news, verified signals from Step 2 | 15-25 prioritized leads with tier classification |
| 4 | **02 — Expansion** | Selects 3-6 leads, expands to 400-800 word stories, enforces Civic Grounding Gate. Checkpoint separates drafting from verification. | Story leads from Step 3 | Publication-ready stories + Suppression Ledger |
| 5 | **05 — Integrity** | Post-production 5-part audit: links, claims, source tiers, voices, completeness. **Universal final gate — ALL stories from ANY prompt must pass here before publication.** | Stories from Step 4 or Prompt 09 | Audit results with publish/hold recommendation |
| 6 | **07 — Translator** | Rewrites approved stories at 8th-grade reading level. | Approved stories from Step 5 | Plain-language versions for publication |

---

## On-Demand Agents (Use When Needed)

| Prompt | When to Use | Input | Output |
|--------|------------|-------|--------|
| **06 — First Amendment Counsel** | Legal threat, access denial, SLAPP suit, records dispute, publication question | Description of the threat or question | Threat triage + legal analysis + immediate actions |
| **09 — Research & Writing** | Ad-hoc story outside the daily pipeline (standalone research + writing). Must pass Prompt 05 before publication. | A topic | Researched, written, and verified news story → Prompt 05 |

---

## Cross-Cutting Protocol (Not Run Independently)

| Prompt | What It Does | Where It's Enforced |
|--------|-------------|-------------------|
| **08 — Civic Grounding** | Anti-plagiarism rules: journalism as leads only, Hard-No-Bluff Rule, 4-question self-check | Embedded in Prompt 02 (Grounding Gate) and Prompt 05 (Source Tier Audit) and Prompt 09 (Grounding Check) |

---

## Templates (Fill In Before First Run)

| Template | Fill In | Used By |
|----------|---------|---------|
| `source-tier-reference.md` | Nothing — shared reference, pre-filled | All prompts |
| `canonical-sources-registry.md` | Your city's source URLs and tiers | Prompt 01 |
| `story-lead-template.md` | Nothing — output format, pre-filled | Prompt 01 |
| `suppression-ledger.md` | Your city name; entries accumulate over time | Prompts 02, 05 |
| `civic-calendar.md` | Your city's meeting schedule and dates | Prompt 01 |
| `corrections-policy.md` | Your city name; entries added when errors found | Post-publication |

---

## Quick Decision Tree

```
Got a legal threat?               → Prompt 06
Want to scan for hidden signals?  → Prompt 03 → 04 → handoff to 01 (daily) or 09 (standalone)
Daily news production run?        → Prompt 01 → 02 → 05 → 07
One-off story on a specific topic? → Prompt 09 → Prompt 05
Story fails grounding?            → Headline-only note OR suppress (Prompt 08 rules)
All stories fail grounding?       → Empty package is acceptable (documented in Suppression Ledger)
Published story has an error?     → corrections-policy.md
```

---

## Platform Requirements

These prompts require a large context window. Not all AI platforms can run them.

| Platform | Free Context Window | Works? |
|----------|-------------------|--------|
| **Gemini** | 1,000,000 tokens | Yes — largest free window |
| **Claude** | 200,000 tokens | Yes — plenty of room |
| **ChatGPT Plus/Pro** | 128K–200K tokens | Yes |
| **ChatGPT Free** | ~8,000 tokens | **No** — smaller than a single prompt |
| **Grok** | No free tier (X Premium required) | Yes with subscription |
| **Perplexity** | Search-focused, not a prompt executor | **No** — wrong tool for this |

If you're starting out, **Gemini (free)** or **Claude (free)** are the recommended platforms.

---

## Source Tier Quick Reference

| Tier | What It Is | Can You Publish From It? |
|------|-----------|------------------------|
| **A** | Official .gov records, meeting transcripts, YouTube transcripts from city channel | YES — only Tier A grounds published claims |
| **B** | School district, transit agency, news outlets | NO — leads only, not sources |
| **C** | Reddit, Nextdoor, social media, blogs | NO — signal generators only |
| **D** | New/unverified sources under 2-week evaluation | NO — probationary |

---

## Confidence Models (Why the Scales Differ)

The pipeline uses four different confidence scales. They are intentionally different because they measure different things at different stages.

| Prompt | Scale | What It Measures | Why This Scale |
|--------|-------|-----------------|----------------|
| **01 — Aggregator** | 0.0–1.0 | Lead potential — how likely is this worth pursuing? | Continuous probability; allows fine-grained ranking of 15-25 leads |
| **03 — Black Desk** | 0.0–0.5 (capped) | Speculative signal strength | Hard cap at 0.5 ensures speculation never registers as high confidence |
| **04 — Dark Signal** | 0.0–1.0 | Signal verification confidence — how well did this survive adversarial testing? | Same continuous scale as Prompt 01, but measuring a different question |
| **02 — Expansion** | 1–10 | Publication readiness — is this story ready to print? | Integer scale for editorial judgment; conversion from Prompt 01's 0.0–1.0 is defined in Prompt 02's confidence table |

These are not the same scale applied inconsistently. A lead at 0.85 confidence (Prompt 01) becomes a story at 7/10 readiness (Prompt 02) because "worth pursuing" and "ready to publish" are different judgments.
