# How to Find Your City's Sources

**A step-by-step guide to building a Canonical Sources Registry for any municipality. This is the first thing you should do before running any prompts.**

---

## Step 1: Find Your City's Official Website

Search: `[your city name] [your state] official website`

Most city websites follow patterns like:
- `cityname.gov`
- `cityofname.gov`
- `cityname.org`
- `ci.cityname.state.us`

**What to look for on the homepage:**
- "News" or "Announcements" section (this becomes a Tier A source)
- "Government" or "Your Government" menu
- "Departments" listing
- Search function

---

## Step 2: Find the Agenda/Meeting Portal

This is your single most important source. City council agendas and packets contain the raw decisions that drive local governance.

**Search for:** `[your city name] city council agendas`

**Common agenda platforms** (look for these names in the URL or footer):
- **PrimeGov** — `cityname.primegov.com/public/portal`
- **Granicus/Legistar** — `cityname.legistar.com`
- **Municode** — Often hosts municipal code, sometimes agendas
- **iCompass** — `cityname.icompasstech.com`
- **Boardroom** — Used by some smaller municipalities
- **Custom city portal** — Some cities build their own

**What to look for:**
- Agenda PDFs (the short list of items)
- Packet PDFs (the full supporting documents — this is the gold)
- Minutes from past meetings
- Video recordings of meetings

**If you can't find an agenda portal:** Call your City Clerk's office and ask where council agendas are posted. This is public information; they're required to tell you.

---

## Step 3: Find Your City's Official YouTube Channel

Search: `[your city name] city council YouTube`

Many municipalities post meeting recordings to YouTube. These are a critical source.

**What to look for:**
- The city's official channel (usually named "[City Name] Government" or "[City Name] City Council")
- Full-length meeting recordings (not highlight clips)
- Auto-generated transcripts (click "..." under any video → "Show transcript")

**Why this matters:** YouTube auto-generated transcripts from official city channels are **Tier A sources** — they are machine transcriptions of government proceedings. When meeting minutes haven't been posted yet but the recording is available, the YouTube transcript can ground published claims. Add this channel to your Canonical Sources Registry as a Tier A source with a "daily" or "post-meeting" check frequency.

---

## Step 4: Find Your School District

Search: `[your city name] school district`

**What to look for:**
- Board meeting agendas and minutes
- News/announcements section
- Superintendent communications
- Budget documents

---

## Step 5: Find Your County Government

Search: `[your county name] county [your state] government`

**What to look for:**
- Commissioner/supervisor meeting agendas
- Planning department pages
- Health department announcements
- Economic development news
- GIS/mapping tools (useful for development stories)

---

## Step 6: Identify Your State's Key Portals

Every state has these (names vary):

- **Secretary of State** — Business filings, elections
- **Department of Revenue** — Economic data
- **Department of Local Affairs** — Municipal statistics, housing data
- **Department of Transportation** — Infrastructure projects
- **Open data portal** — Many states have one: `data.[state].gov`

---

## Step 7: Find Community Information Sources

These supplement official sources with ground-level intelligence:

- **Local public media / community radio** — Often covers what papers don't
- **City's official social media** — Facebook, Twitter/X, Nextdoor presence
- **Reddit** — Search for `r/[yourcityname]` — surprisingly useful for anecdotal signals
- **Chamber of Commerce** — Business community news
- **Library system** — Often posts community event listings

---

## Step 8: Identify Regional/Adjacent Sources

Stories don't stop at city limits. Identify:

- **Adjacent municipalities** — Their development decisions may affect your city
- **Regional planning commissions** — Cross-jurisdictional coordination
- **Special districts** — Water, fire, library, parks — often have separate boards
- **Regional transit authority** — Service changes affecting your city

---

## Step 9: Build Your Registry

Now take everything you've found and enter it into the Canonical Sources Registry template (`/templates/canonical-sources-registry.md`).

**Tier assignment guidelines:**

| Tier | Criteria | Check Frequency |
|------|----------|----------------|
| A | Updates daily/weekly, .gov domain or official YouTube channel, city-specific, structured data | Daily or before meetings |
| B | Updates weekly/monthly, authoritative, relevant to your city | Weekly |
| C | Updates monthly or event-triggered, useful for context | When triggered |
| D | Newly discovered, unproven — test for 2 weeks | During testing period |

---

## Tips From Experience

**The best sources are found inside council packets.** Staff reports cite engineering firms, planning consultants, state agencies, and data portals that aren't on any public directory. When you run the News Aggregator, the Source Discovery Module (Part 9) will identify these automatically. But you can also do it manually: read a council packet, note every external organization or document cited, and look them up.

**Check for a city newsletter.** Many cities publish a weekly digest (email or web) that consolidates upcoming events, council agendas, and department updates. This is an excellent planning tool.

**Don't overlook the permit database.** Building permits, business licenses, and code violations are often searchable online. The platform is frequently Accela or CityView. Search: `[your city name] building permits online`

**Public utilities are a separate source.** If your city has a municipal utility, it has its own rate filings, outage reports, and capital plans. If served by a private utility, check the state public utility commission for rate cases.

**Your state's open records law is a fallback.** When online sources fail, you can formally request records. Every state has a public records law (FOIA at the federal level; each state has its own name — CORA in Colorado, CPRA in California, FOIL in New York, etc.). See the FOIA guide in `/guides/filing-public-records-requests.md`.
