# Setup Guide: Platform-by-Platform Instructions

**Detailed instructions for setting up Civic Newsroom on different AI platforms for regular use.**

---

## Option 1: Claude Projects (Recommended for Regular Use)

Claude Projects let you store your prompts and registry as permanent reference documents. You don't need to paste them each time.

### Setup (one time, ~15 minutes):
1. Go to https://claude.ai/projects
2. Click "Create Project"
3. Name it: "[Your City] Civic Newsroom"
4. Click "Add content" and upload these files:
   - Your filled-in `01-news-aggregator.md`
   - `02-story-expansion.md`
   - `03-black-desk.md` (filled in with your city)
   - `04-dark-signal-desk.md`
   - `05-integrity-checker.md`
   - `09-story-research-writing.md`
   - Your `canonical-sources-registry.md`
   - `source-tier-reference.md`
   - `corrections-policy.md`
   - `PIPELINE-CHEAT-SHEET.md`
5. Save the project

### Daily use:
1. Open your project
2. Start a new chat
3. Say: "Run the news aggregation for [your city]"
4. Review the output, select leads, then say: "Expand lead #3 and #7 into full stories"
5. Say: "Run the integrity checker on those stories"

---

## Option 2: ChatGPT Custom GPT

Custom GPTs can store your instructions as permanent system prompts.

### Setup (one time, ~20 minutes):
1. Go to https://chat.openai.com → Explore GPTs → Create
2. Name it: "[Your City] Civic Newsroom"
3. In the Instructions field, paste your filled-in News Aggregator prompt
4. Upload your canonical sources registry as a Knowledge file
5. Save and publish (private)

### Daily use:
1. Open your Custom GPT
2. Say: "Run the daily aggregation"
3. For story expansion, start a new chat and paste the Story Expansion prompt with your leads

### Limitation:
Custom GPTs have a single instruction field, so you'll need separate GPTs for different agents (aggregation, Black Desk, etc.) or switch prompts manually.

---

## Option 3: Copy/Paste (Works Everywhere)

The simplest approach. Save your filled-in prompts as text files and paste when needed.

### Setup (one time, ~10 minutes):
1. Fill in the `[BRACKETED]` variables in each prompt file with your city's info
2. Save each filled-in prompt as a separate text file on your computer or in Google Docs/Notes
3. Keep your canonical sources registry in a document you update regularly

### Daily use:
1. Open Claude, ChatGPT, or Gemini
2. Paste the relevant prompt
3. Run it
4. Copy/paste output to wherever you publish

### Pros:
- Works on any platform
- No setup required beyond filling in variables
- You control everything

### Cons:
- Requires pasting each time (~30 seconds)
- No persistent memory between sessions

---

## Option 4: Claude Cowork Mode (Advanced)

If you're using Claude's Cowork desktop mode, you can set up the prompts as skills.

### Setup:
1. Save your filled-in prompts to your working folder
2. Claude can read them directly and execute the full pipeline
3. Results get saved as files you can review and publish

This is the most automated option but requires the Claude desktop app.

---

## Organizing Your Output

However you set up the system, you'll want a consistent place to store output:

### Suggested folder structure:
```
my-civic-newsroom/
├── prompts/           # Your filled-in prompt files
├── registry/          # Your canonical sources registry (update regularly)
├── templates/         # Corrections policy, suppression ledger, civic calendar
├── output/
│   ├── 2026-03/       # Organized by month
│   │   ├── 2026-03-10-leads.md
│   │   ├── 2026-03-10-stories.md
│   │   └── 2026-03-10-suppression-ledger.md
│   └── ...
├── black-desk/        # Weekly Black Desk outputs
├── corrections/       # Corrections log entries (see corrections-policy.md)
└── sources-log/       # New source discoveries
```

### Naming convention:
`YYYY-MM-DD-[type].md`
- `2026-03-10-leads.md` — Aggregation output
- `2026-03-10-stories.md` — Expanded stories
- `2026-03-10-black-desk.md` — Black Desk scan
- `2026-03-10-integrity-check.md` — Integrity audit results

---

## Publishing Options

Once you have publication-ready stories, you need somewhere to put them:

- **Substack** — Free newsletter platform, good for building a local audience
- **WordPress** — Free or cheap, more control over presentation
- **Medium** — Easy publishing, built-in audience (limited local reach)
- **Ghost** — Open-source publishing platform
- **Nextdoor** — Posting summaries can reach local residents directly
- **City Facebook groups** — Where many residents already get local info
- **Your own domain** — Most professional, full control

The stories are yours. Publish them however makes sense for your community.
