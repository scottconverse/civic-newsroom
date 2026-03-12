# Source Tier Reference

**Version:** 2.2
**Last Modified:** March 12, 2026
**Tested With:** Prompts 01, 02, 03, 05, 09 (QA Stress Test, March 12, 2026)

**Shared reference for all Civic Newsroom prompts. When a prompt references "Tier A," "Tier B," or "Tier C" sources, this document defines what those tiers mean.**

---

## Tier A: Primary Government Records

**Confidence threshold:** >= 0.85
**Check frequency:** Daily or before each council meeting

**What qualifies:**

- Official meeting agendas, packets, and minutes
- City council resolutions and ordinances
- Approved budgets and budget amendments
- Building permits, zoning applications, and land use filings
- Signed contracts, procurement awards, and RFP documents
- Audit reports published by city or county auditor
- Court filings and public judicial records
- Official city/county/state press releases
- Audio/video recordings of public meetings (attribute by timestamp)
- Official municipal YouTube channels (livestreams and archives of council
  meetings, board meetings, and public hearings). YouTube auto-generated
  transcripts from these channels are Tier A sources — they are machine
  transcriptions of official government proceedings. Cite with video title,
  channel name, timestamp, and URL. These are second only to agenda portals
  (e.g., PrimeGov) in verification priority: when a meeting packet is not
  accessible, the YouTube transcript of that same meeting grounds the claims.
- Public data portals (.gov, .edu domains with structured data)

**Key rule:** Tier A sources are the only acceptable basis for publication. If a claim cannot be traced to a Tier A source, it requires either additional verification or a headline-only note.

---

## Tier B: Institutional and Verified Secondary Sources

**Confidence threshold:** 0.75-0.84
**Check frequency:** Weekly

**What qualifies:**

- School district official communications and board materials
- Transit agency service announcements and project updates
- County commission news and regional planning documents
- State regulatory filings affecting the city
- Established local news outlets with original reporting (as leads, not sources — see Prompt 08)
- Chamber of Commerce or economic development authority publications
- University research and reports specific to the city/region
- Named official statements on social media (verified accounts only)

**Key rule:** Tier B sources provide context and lead generation. They may corroborate Tier A findings but should not be the sole basis for a published factual claim.

---

## Tier C: Community and Anecdotal Sources

**Confidence threshold:** 0.65-0.74 (conditional use)
**Check frequency:** Conditional / event-triggered

**What qualifies:**

- Reddit community posts and threads (city subreddits)
- Nextdoor neighborhood discussions
- YouTube comments on council meeting recordings
- Facebook community group posts
- Google Maps reviews for city offices/services
- Local blog posts and opinion pieces
- Unverified social media reports
- Anonymous tips or complaints

**Key rule:** Tier C sources are signal generators, not evidence. They tell you WHERE to look, not WHAT to publish. The Black Desk (Prompt 03) uses Tier C as starting points. The Dark Signal Desk (Prompt 04) requires Tier A/B verification before any Tier C signal can advance. Tier C sources should never appear as the sole attribution for a published claim.

---

## Tier D: Experimental / Under Evaluation

**Confidence threshold:** 0.55-0.64
**Evaluation period:** 2 weeks minimum

**What qualifies:**

- Newly discovered sources that pass 5/7 of the validation checklist (Prompt 01, Part 9) but have not been tested over time
- Sources from adjacent jurisdictions that may be relevant
- Data portals with incomplete or irregular update schedules

**Key rule:** Tier D sources are on probation. Track their output for 2 weeks. If they produce actionable leads with verifiable data, promote to Tier C or above. If not, move to Rejected.

---

## How Tiers Flow Through the Pipeline

```
Black Desk (Prompt 03)        → Uses Tier C as starting points, anchored to Tier A/B
Dark Signal Desk (Prompt 04)  → Requires Tier A/B for verification; Tier C only if verified
News Aggregator (Prompt 01)   → Prioritizes Tier A; supplements with Tier B/C for leads
Story Expansion (Prompt 02)   → Requires Tier A attribution for all published claims
Integrity Checker (Prompt 05) → UNIVERSAL FINAL GATE: audits against Tier A; all stories must pass here
Research & Writing (Prompt 09) → Built-in Civic Grounding Check; requires Tier A; must pass Prompt 05
```
