# Canonical Sources Registry

**City:** [YOUR_CITY], [YOUR_STATE]
**Version:** 2.0
**Last Modified:** March 11, 2026
**Tested With:** Prompt 01 Part 9 (QA Stress Test, March 12, 2026)
**Last Updated:** [DATE]
**Total Active Sources:** [NUMBER]

---

## About This Registry

This is the "memory" of your civic reporting system. It organizes all validated sources by reliability tier, tracks performance, documents rejected sources to prevent re-evaluation waste, and feeds back into your aggregation prompts each run.

**Update Frequency:**
- Weekly reviews (Tier D experimental sources)
- Monthly audits (all tiers, first Monday of month)
- Quarterly deep cleaning (remove stale sources)

---

## TIER A: CORE DAILY/WEEKLY SOURCES

**Required:** Confidence >= 0.85 | Update frequency: Daily or Weekly

### SOURCE: [City Agenda Portal]
- **URL:** [URL]
- **Category:** Civic - Government
- **Added:** [DATE]
- **Update Frequency:** [Daily/Weekly — e.g., agendas posted 5-7 days before meetings]
- **Data Type:** Meeting agendas, packets, minutes
- **Check Trigger:** [e.g., Before each council meeting]
- **Confidence:** [0.0-1.0]
- **Notes:** [Access notes, any robots.txt issues, login requirements]
- **Last Verified:** [DATE]
- **Leads Generated (Last 30 days):** [NUMBER and examples]

---

### SOURCE: [City Official News Page]
- **URL:** [URL]
- **Category:** Civic - Government
- **Added:** [DATE]
- **Update Frequency:** Daily
- **Data Type:** Press releases, announcements, alerts
- **Check Trigger:** Daily morning check
- **Confidence:** [0.0-1.0]
- **Notes:** [Details]
- **Last Verified:** [DATE]
- **Leads Generated (Last 30 days):** [NUMBER]

---

### SOURCE: [School District]
- **URL:** [URL]
- **Category:** Civic - Education
- **Added:** [DATE]
- **Update Frequency:** [Weekly/Biweekly]
- **Data Type:** News, board meetings, programs
- **Check Trigger:** [e.g., Weekly Tuesday/Friday checks]
- **Confidence:** [0.0-1.0]
- **Notes:** [Details]
- **Last Verified:** [DATE]
- **Leads Generated (Last 30 days):** [NUMBER]

---

[Add more Tier A sources as discovered]

---

## TIER B: REGULAR WEEKLY SOURCES

**Required:** Confidence 0.75-0.84 | Update frequency: Weekly

### SOURCE: [County Government]
- **URL:** [URL]
- **Category:** Regional - Government
- **Added:** [DATE]
- **Update Frequency:** Weekly
- **Data Type:** Commission news, regional planning
- **Check Trigger:** Weekly
- **Confidence:** [0.0-1.0]
- **Notes:** [Details]
- **Last Verified:** [DATE]

---

### SOURCE: [Transit Agency]
- **URL:** [URL]
- **Category:** Infrastructure - Transit
- **Added:** [DATE]
- **Update Frequency:** Monthly / As-needed
- **Data Type:** Service changes, infrastructure projects
- **Check Trigger:** Monthly or when service changes announced
- **Confidence:** [0.0-1.0]
- **Notes:** [Details]
- **Last Verified:** [DATE]

---

[Add more Tier B sources]

---

## TIER C: CONDITIONAL/EVENT-TRIGGERED SOURCES

**Required:** Confidence 0.65-0.74 | Check when specific events trigger

### SOURCE: [State Government Portal]
- **URL:** [URL]
- **Category:** State - Policy
- **Added:** [DATE]
- **Check Trigger:** When state legislation affects your city
- **Confidence:** [0.0-1.0]
- **Notes:** [Details]
- **Last Verified:** [DATE]

---

[Add more Tier C sources]

---

## TIER D: EXPERIMENTAL / UNDER EVALUATION

**Required:** Confidence 0.55-0.64 | Two-week testing period

### SOURCE: [Name]
- **URL:** [URL]
- **Category:** [Category]
- **Added:** [DATE]
- **Testing Period:** [START - END]
- **Evaluation Criteria:** [What would make this Tier C or above?]
- **Notes:** [Details]

---

## REJECTED SOURCES

**Document to avoid re-checking in future runs.**

### REJECTED: [Source Name]
- **URL:** [URL]
- **Rejection Date:** [DATE]
- **Rejection Reason:**
  - [ ] Outdated (last update >6 months ago)
  - [ ] Paywall/login required
  - [ ] Not city-specific
  - [ ] Low-quality data
  - [ ] Duplicate of existing source
  - [ ] Irregular updates
  - [ ] Other: [specify]

---

[Add more rejected sources as encountered]
