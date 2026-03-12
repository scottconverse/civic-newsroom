# I Built an AI-Powered Civic Transparency System for My City. Now I'm Giving It Away.

*An open-source system that turns any city's public records into accessible civic reports — using tools you already have.*

---

In 2005, there were roughly 9,000 newspapers in the United States. Today, there are fewer than 6,000. More than 2,500 communities have lost their local paper entirely. The places they covered didn't stop making decisions. City councils still meet. Budgets still get passed. Zoning variances still get approved. Contracts still get awarded.

But in most of these communities, nobody is reading any of it.

I know because I live in one. Longmont, Colorado, population 105,000, has a city council that meets twice a month, a school district with a billion-dollar budget, and a county government making regional planning decisions that affect tens of thousands of residents. The city publishes 200-page council packets before every meeting. The information is technically public.

Almost nobody reads it.

I decided to build a system that does.

---

## What I Built

Over the last several months, I developed what I call the Civic Newsroom — a nine-agent AI pipeline that turns public records into accessible civic reports. It's not a single chatbot prompt. It's a complete editorial system:

An **aggregator** that scans city agendas, government portals, and school district websites to produce 15-25 story leads daily.

A **story expansion engine** that converts the best leads into publication-ready civic reports with proper attribution, neutral tone, and full sourcing.

A **speculative signal radar** (I call it the Black Desk) that looks for what's NOT there — the report that was promised but never appeared, the meeting item that was withdrawn without explanation, the neighborhood where complaints cluster but services don't arrive. It detects signals nobody else is watching.

A **structured verification desk** with a mandatory adversarial four-gate protocol that forces the system to hunt for counter-narratives before any contested claim can move toward publication.

An **integrity checker** with publication-readiness thresholds that distinguish critical factual errors from minor attribution issues, verify contact attempts for "no response" claims, and provide clear hold/publish/correct guidance before any story goes live.

An **anti-plagiarism protocol** that ensures reporting is grounded in primary public records — not rewritten from other journalists' work — with clear definitions of what counts as a primary source.

A **First Amendment counsel** for legal guidance on press freedom, public records access, and defamation risk — with plain-language definitions of legal concepts like "actual malice."

A **plain-language translator** that rewrites civic jargon into English regular people can understand, including failure-path explanations for conditional policies.

I ran this system against live municipal data in Longmont. It produced real stories. More importantly, it taught me exactly how AI-assisted journalism can fail — and I built every lesson into the architecture.

---

## Why the Safeguards Exist

AI-assisted journalism can fail in specific, predictable ways. I designed this system to prevent each of them architecturally.

**AI will hallucinate.** Large language models generate factual errors — fabricated quotes, incorrect dates, misattributed claims. This is a structural property of how they work, not a defect in any particular model. To prevent hallucination from reaching publication, I built the adversarial verification protocol — a mandatory four-gate system that cannot be bypassed. Before any contested signal can be finalized, the system must search for counter-narratives across at least 3 platforms within a 90-day window, document every search attempt (including failed queries), and present competing truth claims without picking a side. The Integrity Checker adds a second layer with defined publication-readiness thresholds.

**AI will produce one-sided analysis.** Without explicit counter-narrative searching, an AI system will naturally analyze contested situations from whatever perspective is most available — producing analysis that's coherent, well-sourced from one side, and dangerously incomplete. The adversarial protocol forces the system to actively hunt for the other side before any signal can move toward publication.

**AI will inadvertently plagiarize.** Without guardrails, AI synthesizes available information — including other journalists' reporting — into narratives that look like original work but are actually rewrites. The Civic Grounding Protocol ensures every claim traces back to primary public records — including official municipal YouTube channel transcripts, which are machine transcriptions of government proceedings. Other outlets' work can tell you what to look for, but it can never be your source. When their reporting did lead you to a story, a mandatory Journalism Credit in the closing paragraph acknowledges their work.

---

## Why I'm Giving It Away

Every community with a city council and a public records portal can benefit from these tools. The system to make public records accessible doesn't need to be proprietary. It needs to be available to anyone who wants to use it.

So today I'm open-sourcing the entire thing. Every prompt. Every protocol. Every template. Every guide. The adversarial verification system. The anti-plagiarism safeguards. The suppression ledger methodology. All of it.

---

## What You Get

The **Civic Newsroom** repository contains everything you need to stand up a functioning AI-powered civic reporting operation for your city:

**Nine generalized prompts** — the complete editorial pipeline, with `[YOUR_CITY]` variables you fill in for your municipality.

**Six blank templates** — Canonical Sources Registry, story lead format, suppression ledger with revision pathways, civic calendar, a shared Source Tier Reference defining the confidence hierarchy used across all nine agents, and a corrections policy for post-publication error handling.

**A pipeline cheat sheet** — one-page reference showing the canonical prompt order, what each agent expects and produces, and a quick decision tree.

**Guides for people who've never done this before** — how to find your city's public records sources, how to read a council packet, how to file public records requests, the anti-plagiarism protocol, the adversarial verification system.

**A working example** — the complete Longmont, Colorado configuration, with real sources, real meeting schedules, and notes from actual operation.

You don't need to be a journalist. You don't need to code anything. You need a free AI chatbot account, your city's council agenda URL, and the willingness to read what your city government is actually doing.

---

## How to Start

1. Clone or download the repository
2. Read the Quickstart guide (10 minutes)
3. Find your city's four key URLs: agenda portal, official news page, school district, and official YouTube channel
4. Fill in the News Aggregator prompt with your city's info
5. Paste it into Claude, ChatGPT, or Gemini
6. Read what comes back

Your first run will produce 15-25 story leads drawn from your city's public records. Some will be routine. Some will surprise you.

---

## The Ask

Try it in your town.

If you set it up for your city, contribute your configuration back to the repository so others can see how it's done in different municipalities with different platforms.

If you find ways to make the prompts better, submit improvements.

If you publish stories using this system, tell us about it.

The information to hold local government accountable already exists in public records. What's been missing is someone reading them. Now there's a system for that.

And it's yours.

---

**Repository:** [https://github.com/scottconverse/civic-newsroom](https://github.com/scottconverse/civic-newsroom)

**License:** MIT — use it, fork it, adapt it, improve it, share it.

**Author:** Scott Converse — founder of ClickCaster (sold 2008), co-founder of The Longmont Observer, builder of the Longmont News Network civic intelligence pilot.
