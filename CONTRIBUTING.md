# Contributing to Civic Newsroom

Thank you for your interest in making this project better. Here's how you can help.

---

## Add Your City

The most valuable contribution is a working configuration for your city. If you've set up Civic Newsroom for your municipality, submit a PR adding your city to the `/examples/` directory.

### What to include:

Create a folder: `/examples/[your-city]-[your-state]/`

Include:
- **sources-registry.md** — Your canonical sources registry with at least Tier A and B sources filled in (remember: official municipal YouTube channel transcripts are Tier A)
- **civic-calendar.md** (optional) — Your city's meeting schedule
- **corrections-policy.md** (optional) — Your filled-in corrections policy, if you've customized it
- **notes.md** (optional) — Anything you learned that would help others in similar cities (e.g., "This city uses Granicus and packets are only posted 3 days before meetings" or "The permit database requires a free account to search")

### What NOT to include:
- Personal information or login credentials
- Copyrighted content from news outlets
- Output from your aggregation runs (keep that for your own use)

---

## Improve the Prompts

If you've found ways to make the prompts work better — whether through testing on different LLM platforms, handling edge cases, or improving the output format — submit a PR with your changes.

Please include:
- What you changed and why
- Which platform(s) you tested on
- Before/after examples if possible

---

## Improve the Guides

If you found a step confusing, discovered a better way to find sources, or have experience with public records requests in your state, improve the guides.

---

## Report Issues

If something doesn't work as described, open an issue with:
- Which prompt and which section
- What platform you're using
- What happened vs. what you expected
- Any error messages or unexpected output

---

## Code of Conduct

This project exists to strengthen civic transparency. Contributions should be:
- Made in good faith
- Focused on accuracy and public benefit
- Respectful of existing local journalists and news outlets

We don't accept contributions that:
- Undermine other journalists' work
- Target specific individuals or organizations
- Promote partisan or advocacy goals over factual reporting

---

## License

By contributing, you agree that your contributions are licensed under the MIT License.
