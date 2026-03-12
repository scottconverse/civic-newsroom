# Why This Exists

## The Problem

Since 2005, more than 2,500 U.S. newspapers have closed. The places they covered didn't stop generating public records. City councils still meet. Budgets still get passed. Zoning variances still get approved. Contracts still get awarded. Public comment periods still open and close.

But in more and more communities, nobody is reading any of it.

This isn't a technology problem. It's a structural failure. Municipal governments produce millions of pages of actionable public information every year. That information is technically available — posted on portals, buried in agenda packets, filed in permit databases, scattered across dozens of department websites. But "technically available" and "functionally accessible" are very different things.

A 200-page city council packet posted as a PDF five days before a vote is not journalism. It's a filing. For it to become journalism, someone has to read it, identify what matters, verify the claims, find the affected people, and write it in language a resident can act on.

That "someone" used to be a beat reporter at the local paper. In most American communities, that person no longer exists.

## What We Built

Civic Newsroom is a system — not a single tool — for turning public records into accessible civic reports using AI.

It's nine coordinated agents, each handling a different part of the civic reporting process:

**Signal detection** — scanning municipal portals, agendas, official YouTube channels, and community discourse for story leads. Not searching the web randomly, but methodically checking the specific sources where your city's decisions are documented. A Serial Coverage Tracker maintains active threads for multi-week civic stories so nothing falls through the cracks between runs.

**Speculative intelligence** — looking for what's *not* there. The report that was promised but never appeared. The meeting item that was withdrawn without explanation. The neighborhood where complaints cluster but services don't. The fiscal transfer buried in a consent agenda. Most journalism finds stories in what happened. This layer finds them in what didn't.

**Adversarial verification** — a mandatory four-gate protocol that forces the system to actively hunt for counter-narratives before any contested signal moves forward. The protocol requires searching a minimum of 3 platforms within a 90-day window using at least 3 query variations, and documenting every search attempt — including failed queries. Without this gate, an AI system will naturally produce one-sided analysis of contested situations — coherent, well-sourced from one perspective, and dangerously incomplete. The protocol exists to make that failure mode structurally impossible.

**Story expansion** — converting verified leads into publication-ready civic reports using inverted pyramid structure, proper attribution, and neutral tone. Every claim sourced. Every quote attributed. Every future-tense statement hedged appropriately.

**Integrity auditing** — a post-production check that tests every link, audits every factual claim, flags every missing voice, and identifies every unresolved question before a story can be published. Flags are now split into CRITICAL (factual errors that change meaning) and MINOR (non-material attribution issues), with clear publication-readiness thresholds: HOLD if more than 30% of claims are flagged or any lede claim is unverified, PUBLISH WITH CORRECTIONS for minor-only issues, PUBLISH AS-IS when clean.

**Anti-plagiarism safeguards** — hard rules ensuring that reporting is grounded in primary public records, not rewritten from other journalists' work. Other outlets' coverage can tell you what to look for. It cannot be your source. When a Tier B outlet's reporting did lead you to the story, a mandatory Journalism Credit in the closing paragraph credits their work. This applies to every agent that can produce publishable text — including the standalone Story Research & Writing agent, which now has its own built-in Civic Grounding Check.

**A suppression ledger** — because killing a story is a decision that should be documented. Every suppressed story gets a record: why it was killed, what was missing, and what would make it publishable. Nothing disappears silently. Suppressed stories now include a defined revision pathway — a structured process for addressing specific failures, re-running verification checks, and reopening stories when evidence appears.

## What We Learned

### Lesson 1: AI Will Hallucinate. Build the Catch.

Any AI system generating text about real events will eventually produce factual errors — fabricated quotes, incorrect dates, misattributed claims. This is not a bug in any particular model. It is a structural property of how large language models work. If you're building an AI-powered civic reporting system, assume the AI will be wrong. Don't assume you'll catch it manually.

To prevent hallucination from reaching publication, we built the adversarial verification protocol as a mandatory gate — not an optional step. Every contested signal must pass through a four-gate check that includes counter-narrative searches across at least 3 platforms within a 90-day window, documentation of competing truth claims, and extra scrutiny for self-referential topics. The gate cannot be bypassed. If it isn't passed, the signal cannot be finalized. The Integrity Checker adds a second layer with defined publication-readiness thresholds that distinguish critical factual errors from minor attribution issues.

### Lesson 2: Plagiarism Is Structural, Not Intentional

AI naturally synthesizes available information — including other journalists' reporting — into coherent narratives. Without architectural guardrails, the result can look like original work but actually be a rewrite of someone else's journalism. This isn't intentional plagiarism. It's the AI doing what AI does. But the result is the same.

The fix isn't a disclaimer. It's architectural. The Civic Grounding Protocol forces every story to trace its claims back to primary public records — including official municipal YouTube channel transcripts, which are machine transcriptions of government proceedings and qualify as Tier A sources. If a fact can't be sourced to a government document, meeting record, YouTube transcript, or official announcement, it doesn't go in the story. Journalism from other outlets serves as a lead generator — it tells you what to look for — but it can never be the source. When journalism did lead you to the story, a mandatory Journalism Credit ensures the originating outlet is acknowledged.

### Lesson 3: Speculation Has to Be Separated From Verification

The Black Desk (speculative signal radar) and the Dark Signal Desk (structured verification) exist as deliberately separate agents because mixing speculation with verification is how you publish rumors as facts.

The Black Desk is fail-open by design. Its confidence scores are capped at 0.5 — permanently. It's looking for the dog that didn't bark, for the correlation that might mean something, for the anecdote that might be the start of a pattern. Suppressing speculation at this stage kills stories before they start.

But speculation cannot move toward publication without passing through mandatory adversarial verification. The Dark Signal Desk applies a four-gate protocol: contestation check, adversarial search, documentation of competing truth claims, and a self-referential warning gate for stories about AI or journalism itself (where the system is most likely to have blind spots).

This separation — speculate freely, verify ruthlessly — is the core architectural insight. A shared Source Tier Reference now provides consistent definitions across all agents: Tier A (primary government records — including agendas, minutes, budgets, permits, resolutions, audits, contracts, official press releases, meeting recordings, and official municipal YouTube channel transcripts), Tier B (institutional sources), Tier C (community signals), and Tier D (experimental sources under evaluation), each with defined confidence thresholds and usage rules.

### Lesson 4: The Suppression Ledger Is as Important as the Published Story

A reporting system that can't explain why it *didn't* publish something is a system that can't be trusted. The suppression ledger documents every killed story: what was missing, why it couldn't be verified, what evidence would make it publishable.

This serves two purposes. First, it creates accountability — you can audit not just what was published but what was suppressed. Second, it creates a research pipeline — suppressed stories are future leads. When the missing document finally appears, or the source finally goes on record, the ledger tells you which story to reopen. A formal revision pathway now structures this process: address the specific failure, re-run the appropriate verification check, update the ledger status, and move the story back into publication if it passes.

An important corollary: a day with zero publishable stories is an acceptable outcome. If every lead fails the Civic Grounding Gate, the system produces an empty story package with a complete Suppression Ledger. A blank package with honest documentation is better than a package with stories that violate the anti-plagiarism safeguards.

### Lesson 5: Published Errors Need a Formal Process

No verification system catches everything. When an error makes it through to publication, a Corrections Policy provides the framework: what requires a correction vs. a retraction, the exact format for public corrections, and a running Corrections Log that documents every post-publication fix. Root cause analysis is built in — each correction triggers an investigation into which safeguard missed it and how to prevent recurrence.

## The Design Principle

The system follows one rule: **fail-open for collection, fail-closed for publication.**

Cast a wide net. Capture signals from public records, social media, community forums, budget documents, permit databases. Let noise in. Let speculation in. Let correlations in. Let absences in.

Then close the gates. Every signal that moves toward publication must pass through adversarial verification, integrity checking, anti-plagiarism safeguards, and a completeness audit. The Integrity Checker (Prompt 05) serves as the universal final gate — no story from any prompt, whether daily production or standalone research, is publication-ready until it has passed that independent audit. No prompt can self-certify its own output. If a story can't pass, it gets suppressed — documented, but suppressed.

The pipeline is not designed to maximize output. It's designed to maximize trust.

## Why Open Source

Every community with a city council and a public records portal can use these tools to make government decisions more accessible. The system doesn't need to be proprietary. It needs to be available to anyone who wants to use it.

If you live in a town where the local paper closed, or shrank to the point where nobody covers city council anymore, you now have the same system that was developed and refined against live municipal data. It's not perfect. It carries its safeguards openly. But it works.

Take it. Adapt it to your city. Run it. Improve it. Share what you learn.

The information is already public. It just needs someone reading it.
