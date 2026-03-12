# Quickstart: Get Running in 30 Minutes

**This guide gets you from zero to your first civic news aggregation run. You need: an AI chatbot account (Claude, ChatGPT, or Gemini) and 30 minutes.**

---

## Step 1: Pick Your City (2 minutes)

Decide which municipality you want to cover. This works for any city, town, or county in the United States that publishes meeting agendas online (which is nearly all of them).

## Step 2: Find Four Things (10 minutes)

You need four URLs to get started. Open your browser and find:

**A. Your city's agenda/meeting portal**
Search: `[your city] city council agendas`
Look for platforms like PrimeGov, Granicus, Legistar, or the city clerk's page.

**B. Your city's official news page**
Search: `[your city] official website news`
Usually at `[cityname].gov/news` or similar.

**C. Your school district's website**
Search: `[your city] school district`

**D. Your city's official YouTube channel**
Search: `[your city] city council YouTube`
Many municipalities post meeting recordings to YouTube. The auto-generated transcripts from these recordings are Tier A sources — they're machine transcriptions of official government proceedings and can ground published claims even when meeting minutes haven't been posted yet.

Write down all four URLs.

## Step 3: Fill In the Aggregator Prompt (10 minutes)

1. Open `/prompts/01-news-aggregator.md`
2. Replace these variables with your city's information:
   - `[YOUR_CITY]` → Your city name
   - `[YOUR_STATE]` → Your state
   - `[YOUR_CITY_AGENDA_PORTAL_URL]` → The URL from Step 2A
   - `[YOUR_CITY_NEWS_URL]` → The URL from Step 2B
   - `[YOUR_SCHOOL_DISTRICT]` and `[YOUR_SCHOOL_DISTRICT_URL]` → From Step 2C
   - For the remaining sources (transit, county, state, local media), either fill them in now or delete those sections — you can add them later

3. Fill in the Civic Calendar section with your council's meeting schedule (check the city website for dates/times). If you can't find it quickly, skip this section for now.

## Step 4: Run It (5 minutes to start, ~70 minutes to complete)

1. Open Claude (claude.ai), ChatGPT, or Gemini
2. Paste the entire filled-in prompt
3. Let it run

The AI will scan your city's sources and produce 15-25 prioritized story leads.

## Step 5: Read the Output

Review the leads. Each one includes:
- A headline and intelligence paragraph
- Source URLs
- Three story angles
- Key contacts
- Recommended next steps
- A confidence score

Pick the 3-5 strongest leads (confidence 0.75 or higher).

## Step 6: Expand the Best Leads (Optional)

Take your selected leads, open `/prompts/02-story-expansion.md`, paste it into a new conversation along with the leads, and let it expand them into full stories.

Then run `/prompts/05-integrity-checker.md` on each story before publishing.

---

## What to Do Next

**After your first run:**
- Start building your Canonical Sources Registry using `/templates/canonical-sources-registry.md`
- Add any new sources the aggregator discovered
- Read the council packet guide at `/guides/how-to-read-a-council-packet.md`
- Review the Pipeline Cheat Sheet (`/PIPELINE-CHEAT-SHEET.md`) for the canonical order and quick decision tree
- Set up your Corrections Policy using `/templates/corrections-policy.md` — you'll need this before you publish

**For ongoing coverage:**
- Run the aggregator 2-3 times per week, timed around council meetings
- Run the Black Desk (`/prompts/03-black-desk.md`) weekly to scan for signals
- Keep your sources registry updated
- Check the Serial Coverage Tracker (Part 10 of the Aggregator) to follow multi-week stories

**For contested stories:**
- Always run the Dark Signal Desk (`/prompts/04-dark-signal-desk.md`) with its adversarial verification on any signal involving accusations or conflicting accounts
- Always run the Integrity Checker (`/prompts/05-integrity-checker.md`) before publishing

---

## Platform Tips

### Claude (Anthropic)
- Best option for long, complex prompts — handles the full aggregator well
- Use Claude Projects to keep your prompts and registry permanently available
- Web search works well for source checking

### ChatGPT (OpenAI)
- Works well with all prompts
- Custom GPTs can store your prompts for reuse
- Web browsing mode helps with source verification

### Gemini (Google)
- Good for web-connected research
- May handle some source fetching differently
- The Gemini version of the prompt in the Longmont example was tuned for its specific capabilities

### For All Platforms
- If a prompt is too long for your platform's input limit, split it: run Parts 1-4 first, then Parts 5-9 in a follow-up message
- Save your filled-in prompts as text files so you can reuse them
- Consider setting up a Claude Project or Custom GPT for regular use
