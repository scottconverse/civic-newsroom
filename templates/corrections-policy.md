# Corrections & Retractions Policy

**City:** [YOUR_CITY]
**Version:** 1.0
**Last Modified:** March 12, 2026
**Tested With:** QA Stress Test, March 12, 2026 (created per recommendation 5.3)
**Last Updated:** [DATE]

This policy governs what happens when a published story is later found to contain an error. The Suppression Ledger handles pre-publication kills; this policy handles post-publication errors.

---

## When a Correction Is Required

A correction is required whenever a published story contains a factual error — regardless of how the error was discovered. This includes:

- Incorrect names, titles, dates, vote counts, or dollar amounts
- Misattributed quotes or statements
- Incorrect meeting dates, locations, or agenda item numbers
- Factual claims that were later contradicted by primary source documents
- Source URLs that pointed to the wrong document

A correction is NOT required for:

- Typos or grammatical errors (fix silently in the published version)
- Changes in future plans announced after publication (that's a new story, not an error)
- Differences of interpretation where the original wording was defensible

---

## Correction Format

Publish the correction on the same channel as the original story. Place at the top of the corrected story or as a standalone correction notice.

```
CORRECTION — [DATE]

An earlier version of this story [stated / reported / included] [incorrect information].

What was wrong: [specific error — be precise]
What is correct: [correct information with source]
Source: [Tier A document confirming the correct information]

The story has been updated to reflect the correct information.
[If the error affected the story's core conclusion, note that here.]
```

### Example

```
CORRECTION — March 15, 2026

An earlier version of this story stated that City Council voted 5-2 to approve
the dissolution ordinance. The correct vote was 4-3, according to the official
meeting minutes posted March 14.

What was wrong: Vote count reported as 5-2
What is correct: Vote count was 4-3
Source: City Council Regular Session Minutes, February 24, 2026
(https://longmontcolorado.gov/...)

The story has been updated to reflect the correct vote count.
```

---

## When a Retraction Is Required

A retraction is required when:

- The core factual premise of the story is wrong (not just a detail)
- The story was based on a source that turned out to be fabricated, misidentified, or inapplicable
- The story failed the Civic Grounding Protocol and was published in error (i.e., it should have been caught by Prompts 02, 05, or 08 but wasn't)

A retraction replaces the original story entirely.

```
RETRACTION — [DATE]

This story has been retracted. [Brief explanation of why.]

The original story [stated / reported] [core claim]. Upon review, [explanation
of what was wrong and how it was discovered].

[If a corrected version will be published, note when and where.]

We regret the error.
```

---

## Process

1. **Discovery:** Error is identified (by the operator, a reader, or during a subsequent pipeline run).
2. **Classification:** Determine whether the error requires a correction (detail wrong) or retraction (core premise wrong).
3. **Verification:** Confirm the correct information from a Tier A source before publishing the correction.
4. **Publication:** Post the correction/retraction on the same channel as the original story.
5. **Documentation:** Add an entry to the Corrections Log below.
6. **Root Cause:** Identify which pipeline step should have caught the error. If it's a systemic gap, flag for prompt improvement.

---

## Corrections Log

| # | Date | Story Topic | Error Type | What Was Wrong | Corrected From (Source) | Pipeline Gap |
|---|------|-------------|------------|----------------|------------------------|-------------|
| 1 | [DATE] | [Topic] | Correction / Retraction | [Description] | [Tier A source] | [Which prompt should have caught this] |

---

## Rules

- Never delete the original story without leaving a retraction notice
- Corrections must cite a Tier A source for the correct information — do not correct based on journalism alone
- Time matters: publish corrections as soon as the error is confirmed, not at the next scheduled run
- Transparency over pride: a clear, prompt correction builds trust; hiding errors destroys it
- Log every correction for pattern analysis — repeated errors in the same pipeline step indicate a systemic problem
