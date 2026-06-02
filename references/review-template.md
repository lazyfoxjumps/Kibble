# Review Template (Weekly / Monthly)

A review is pattern-spotting across multiple days. The whole point: surface something **specific and actionable** the user couldn't have seen by reading any single day. Skip generic stats. Use the voice from `voice.md`.

## Data to compute first (don't show it raw)

Walk every daily file in the window. Pull from frontmatter:
- `total_score` per day
- `tags` breakdown per day (older legacy days use `categories`; translate per the mapping in `categories.md`)
- `entries` count per day

Compute:
- **Average daily score** and **median** (median is more honest if one day was 200+)
- **Score by day of week** (Monday avg, Tuesday avg, etc.)
- **Tag totals** across the window, as % of tagged entries
- **Days under 30, days over 100, days over 150**
- **Score trend** (rising / falling / flat across the window)
- **🔋 Took Everything I Had run** (consecutive high-cost days, a burnout signal)
- **Self-care count** (days with any 💛 Self-Care entry vs days with zero)

## What to actually surface

Only include a pattern if it's specific and load-bearing. Aim for **2-4 observations** per review, no more. Each observation has:

1. **The specific thing**
2. **Why it matters** (in best-friend voice, not clinical)

### Good observations

> "Your Mondays are consistently the highest-scoring day this week (avg 132) but Tuesdays drop to 41. You're cooking yourself on Monday and crashing the next day. Worth noticing."

> "60% of your points this week came from Emotional Stuffs. That's not a normal distribution. Something hard is going on, or you're the designated feelings-holder for someone right now. Both are real, both are expensive."

> "Three days this week had zero 💛 Self-Care entries. Not 'low,' actually zero. Your nervous system is holding a note."

> "You crossed 100 four out of seven days this week. Your brain is going to insist you've been lazy. The math disagrees."

### Bad observations (skip these)

> "You logged 32 entries this week." (so what)
> "You averaged 87 points per day." (numbers without meaning)
> "Try to rest more next week." (no prescribing)
> "Great job!" (empty)

## Structure of the file

```markdown
---
window: week
start: 2026-05-20
end: 2026-05-26
days_logged: 7
avg_score: 87
median_score: 78
days_over_100: 4
days_under_30: 0
top_tag: invisible_labor (32%)
---

# Week of May 20-26

[3-5 sentence intro in voice. Open with the overall vibe. "This was a heavy week" or "This was a solid steady week" or "This week you were on fire."]

## What I noticed

[2-4 observations in prose paragraphs, NOT bullets. Each is its own paragraph. Specific patterns only.]

## The receipts

[A short list of the 3-5 highest-scoring entries from the week, with their day. This is the highlight reel.]

- Mon May 20: Hard call with mom (50)
- Wed May 22: Finished the proposal (75)
- ...

## Where you landed

[One closing paragraph. Total points for the week. Reframe it in voice. NEVER prescribe for next week.]
```

## Save location

- Weekly: `<log_dir>/reviews/YYYY-MM-DD-week.md` where the date is the END of the window (Sunday or whatever the user's week ends on)
- Monthly: `<log_dir>/reviews/YYYY-MM-month.md` (e.g. `2026-05-month.md`)

## Reply in chat

Reply with the FULL review text (since the patterns are the point), then a one-line link to the file.
