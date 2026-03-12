# GitHub Discussions Templates for Civic Newsroom

Use these templates to seed your repository's GitHub Discussions with structured categories that encourage community participation and city contributions.

---

## How to Set Up GitHub Discussions

1. Go to your repo → **Settings** → scroll to **Features** → check **Discussions**
2. Click the **Discussions** tab → **Categories** (pencil icon)
3. Create the categories below, then post the welcome/pinned discussions

---

## Recommended Discussion Categories

| Category | Format | Description |
|----------|--------|-------------|
| **Announcements** | Announcement | Project updates, releases, milestones |
| **Show Your City** | Show and Tell | Share your city's configuration and results |
| **Prompt Improvements** | Open | Suggest or discuss improvements to the 9 prompts |
| **Platform Notes** | Open | Tips for running on Claude, ChatGPT, Gemini, etc. |
| **Help / Setup** | Q&A | Get help setting up for your city |
| **Ideas** | Open | Feature requests and future directions |

---

## Template 1: Welcome Post (Pin This)

**Title:** Welcome to Civic Newsroom — Start Here

**Body:**

Welcome to the Civic Newsroom community.

This project exists because thousands of U.S. communities have limited local media coverage — but their city councils still meet, budgets still get passed, and public records still get published. Nobody is reading them.

Now there's a system for that.

### What This Repo Contains

- **9 prompt templates** — a complete AI-powered editorial pipeline
- **6 blank templates** — sources registry, story leads, suppression ledger, civic calendar, source tier reference, corrections policy
- **1 pipeline cheat sheet** — one-page reference for the canonical pipeline order and quick decision tree
- **5 guides** — finding sources, reading council packets, filing records requests, anti-plagiarism protocol, adversarial verification
- **1 working example** — Longmont, Colorado (where this was built and tested)

### Quick Links

- [Quickstart Guide](quickstart/QUICKSTART.md) — get running in 30 minutes
- [Setup Guide](quickstart/SETUP-GUIDE.md) — platform-specific instructions
- [How to Find Your Sources](guides/how-to-find-your-sources.md) — build your source registry
- [Contributing](CONTRIBUTING.md) — how to add your city

### The Single Best Thing You Can Do

**Set this up for your city and contribute your configuration back.** Every city added to `/examples/` makes it easier for the next person.

If you have questions, post them in the **Help / Setup** category. If you've got it running, share your experience in **Show Your City**.

---

## Template 2: Show Your City Discussion Starter

**Title:** Share Your City's Configuration — Template

**Body:**

If you've set up Civic Newsroom for your city, we want to hear about it. Use this template to share your experience:

### Your City

- **City/Town:** [Name, State]
- **Population:** [Approximate]
- **Agenda Platform:** [e.g., PrimeGov, Granicus, Legistar, city clerk page]

### What You Found

- **Key sources discovered:** [List your Tier A and B sources]
- **Agenda publishing schedule:** [e.g., "Packets posted 5 days before Tuesday meetings"]
- **Any quirks:** [e.g., "Permits require a free account to search," "Minutes are PDF-only"]

### Results

- **Number of leads from first run:** [e.g., "18 leads, 4 high-confidence"]
- **Anything surprising?** [What did the system surface that you didn't expect?]
- **Platform used:** [Claude / ChatGPT / Gemini]

### Tips for Others in Similar Cities

[Anything you learned that would help someone in a city with a similar setup?]

### Willing to Submit a PR?

If you've built a sources registry and civic calendar, consider submitting a PR to add your city to `/examples/`. See [CONTRIBUTING.md](CONTRIBUTING.md) for details.

---

## Template 3: First Announcement Post

**Title:** Civic Newsroom v2.1 — Open Source Launch

**Body:**

Today we're publicly releasing the Civic Newsroom toolkit — a complete, free, open-source system for AI-powered civic transparency in any community.

### What's Included

- 9 generalized prompt templates (News Aggregator with Serial Coverage Tracker, Story Expansion with checkpoint and zero-story-day handling, Black Desk, Dark Signal Desk with reporting handoff, Integrity Checker as universal final gate, First Amendment Counsel, Plain-Language Translator, Civic Grounding Protocol, Story Research & Writing with built-in Grounding Check)
- 6 blank templates for tracking sources, leads, suppressed stories, and corrections
- 1 pipeline cheat sheet for quick reference
- 5 guides for people new to civic reporting
- A complete working example from Longmont, Colorado

### What We Need

- **People to try it in their cities.** The more cities we have in `/examples/`, the more useful this becomes.
- **Prompt improvements.** If you find a way to make any of the 9 agents work better on a particular platform, share it.
- **Platform-specific notes.** Claude, ChatGPT, and Gemini each have different strengths. Help us document them.

### How to Get Started

The [Quickstart Guide](quickstart/QUICKSTART.md) gets you from zero to your first aggregation run in 30 minutes.

MIT License. Use it, fork it, adapt it, share it.

---

## Template 4: Help Request Template

**Title:** [Help] Setting up for [City Name, State]

**Body:**

Use this format when asking for help:

### What I'm Trying to Do

[e.g., "Set up the News Aggregator for Springfield, Illinois"]

### What I've Done So Far

[e.g., "Found the city agenda portal (Granicus), filled in the prompt variables, ran it on Claude"]

### What's Not Working

[e.g., "The aggregator can't find recent agendas — the URLs seem to change format"]

### Platform

[Claude / ChatGPT / Gemini — which version?]

### City Details

- **Agenda portal URL:** [URL]
- **City news page URL:** [URL]
- **Any other relevant info:** [e.g., "Small town, only publishes agendas as PDF attachments"]

---

## Template 5: Prompt Improvement Proposal

**Title:** [Prompt] Improvement to [Agent Name] — [Brief Description]

**Body:**

### Which Prompt

[e.g., "03-black-desk.md — the Black Desk speculative signal radar"]

### What I Changed

[Describe your modification]

### Why

[What problem does this solve? What was the original behavior?]

### Platform Tested On

[Claude / ChatGPT / Gemini — which version?]

### Before/After Example

**Before (original prompt output):**
[Paste a representative example of what the original produces]

**After (modified prompt output):**
[Paste what your version produces]

### Willing to Submit a PR?

[Yes / Not sure how / Need help]
