# Changelog

All notable changes to the `kibble` skill (formerly `reverse-todo`).

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versions follow [SemVer](https://semver.org/).

---

## [2.3.0] - 2026-06-05

### Changed (auto-dig is now tag-triggered, not low-total-triggered)

- **The recap auto-dig no longer fires on "brutal low day (total < 30 / spiraling)." It now fires on the 💛 Self-Care tag.** The governing principle: the stash covers *chosen rest*, not *hard-won survival*.
  - At recap, if the day has **at least one entry tagged purely 💛 Self-Care** (no other tag stacked), the stash digs in and fills the bowl **up to 100** (`dig = max(0, 100 − total)`, no-op at/above 100). Any day you genuinely rested gets rounded up to a full bowl.
  - A **💛 + 🔋 stack** ("brushed teeth while depressed") does **not** trigger a dig: it's hard-won effort that already earns real kibble via the bad-day multiplier, and covering it would erase that it was hard. Those points stand on their own.
  - Net effect: the stash now trends *down* over time and only refills on genuine 100+ days, which fixes the "stash piles up forever for no reason" problem.
- **Restorative self-care exception:** a self-care act that *recharges* the user (sleep, nap, drinking water, eating a meal, taking medicine, a bath) is tagged **pure 💛 even on a brutal day**, NOT 💛 + 🔋. The litmus is direction: did the act *cost* them (hard-won shower, dragging through teeth-brushing → 💛 + 🔋, soft dig) or *give something back* (→ pure 💛, full dig). So a depression day whose self-care was "slept, drank water, ate" gets the full round-up to 100. The bad-day scoring multiplier is clarified to be context-driven (not 🔋-gated), so these pure-💛 restorative entries still score generously on a hard day. Updated `categories.md`, `scoring.md`, `SKILL.md`, and `voice.md` (new restorative-on-a-hard-day dig lines).
- **Soft dig (new): hard-won days still get comfort, without erasing the hardness.** When no pure-💛 full dig fires but the day was hard-won (a 🔋 entry, or clearly a struggling day), the pet brings a small handful: `soft_dig = min(15, max(0, 60 − total))`. It never lifts the bowl past the "solid day" line of 60, so the logged score stays honest and the day still reads as the hard day it was. The comfort is the pet showing up, not the number changing. A pure rest day rounds all the way up to 100 (full dig); a hard-won day keeps its low score and gets a hug (soft dig). New voice pool and bowl render added for this case.

### Added (the stash is now spendable, only ever on rest)

- **The stash was a one-way pile (bank surplus, auto-dig on bad days). Now it can be spent on purpose, but only ever on rest, never a points shop.** Three spend paths:
  - **Manual dig (`Mode: dig`)** — user-triggered mid-day top-up when they're drowning, instead of waiting for the recap auto-dig. Triggers: "/kibble dig", "I can't today", "I'm drowning", "dig into the stash". Tops the bowl toward the day's average; same loving beat as the auto dig.
  - **Rest-day claim (`Mode: rest`)** — spend the stash to pre-authorize a guilt-free zero day (today or tomorrow). Triggers: "/kibble rest", "I need a day off", "take tomorrow off", "can I afford a rest day". Marks the day `rest_day: true`, pre-fills the bowl full; recap of a rest day never banks/digs and never reads as a failed day.
  - **"You're loaded" reframe** — a high balance is named in days-off-already-earned terms, not as a number to grow, killing the "piling up for no reason" feeling.
- **Rest-day pricing:** cost = rounded recent average day total (last 7 logged days), floor 50, fallback 100. A rest day costs what a real day costs you.
- **Spend guardrails:** spends are never blocked (balance never below 0); a one-time soft warning fires if a spend would leave reserves low.
- **Ledger** gains a `rest` type and a `trigger` field (`recap` vs `manual`) on digs. Stash stays local-only (not synced).
- New dialogue pools in `voice.md` (manual dig, rest-day claim, "you're loaded", soft warning), new render blocks in `bowl.md`, and a rest-day-claim reaction in both pet files. `recap-template.md` updated to skip bank/dig on claimed rest days.

---

## [2.2.1] - 2026-06-03 (release v1.0.1)

### Fixed

- **Frontmatter key collision with Obsidian.** Renamed the per-tag counts key from `tags` to `tag_counts`, since Obsidian reserves `tags` for its own tag system (a daily file carries both `tag_counts: {...}` for Kibble and Obsidian-native `tags: [kibble, daily-log]`). Updated `SKILL.md`, `sync-obsidian.md`, and `review-template.md`. Also updated the Obsidian frontmatter `tags`/`cssclass` from the legacy `reverse-todo` to `kibble`.

---

## [2.2.0] - 2026-06-03

### Changed (BREAKING: category system replaced)

- **Switched from 6 single-select categories to the handoff's 5 multi-select tags**, Title Cased: 🧠 Invisible Labor, 🔋 Took Everything I Had, 🔁 Routine, 🎨 Creative, 💛 Self-Care. Each entry now gets zero or more tags. 🔋 and 🧠 are intensity flags that stack; 🔋 drives the bad-day scoring multiplier.
- **Frontmatter** `categories: {...}` (summed scores) replaced by `tags: {...}` (entry counts per tag). `total_score` unchanged. Entries can list multiple tags, e.g. `[🧠 invisible labor, 🔋 took everything i had]`. Untagged entries allowed.
- Rewrote `categories.md`, updated `config.json`/`config.example.json`, `SKILL.md`, `scoring.md`, `recap-template.md`, `review-template.md`, `sync-notion.md`, and `README.md` to the tag system.

### Notion

- Added 4 new number columns to the "Kibble" DB (Invisible Labor, Took Everything I Had, Routine, Creative); reused the existing Self-Care column. Legacy category columns (Small Tasks, Emotional Stuffs, Big Brain Hours, Creative Time, Rest) left in place for history, no longer written for new days. Non-destructive.

### Migration

- Existing daily logs left as-is (legacy 6 categories). Reviews translate them via the mapping in `categories.md`. New system applies going forward.

---

## [2.1.1] - 2026-06-03

### Changed

- **Witty, never snarky** added as a voice rule; humor points at the situation or the brain-lie, never at the user or the pet.
- **Never insult the pet** (it's secretly the user): fixed the "affectionately roasted" instruction that produced mean output, added hard bans on snark and pet insults.
- **Warm over stern pass**: softened the brain-lying callout, overflow recap pool, close lines, and self-sabotage pool away from clipped command stacks ("Don't let it. Look at the list.") toward reassuring, friend-with-a-hand-on-your-shoulder phrasing. Anti-gaslight function intact, tone much friendlier.

---

## [2.1.0] - 2026-06-03

### Added

- **Pet personality files** `references/pet-dog.md` and `references/pet-cat.md`: full temperament, tiered sound vocab (the pet never talks, it woofs/meows in styles), tiered action vocab (*tail wag*, *slow blink*, *flops over*), and special-event reactions (onboarding, overflow, stuffed, food coma, hard day, stash bury, stash dig-in, no-future-task bounce). 8-12 rotatable variants per tier. Loaded at runtime per `pet.type`.
- **Narrator and pet interaction pools** in voice.md: the best friend now occasionally talks to the pet ("Biscuit, sit, you'll get more in a sec"), about the pet ("look at him go"), and narrates actions ("scooping you extra for that one"), with tier-tied beats (at 200+ the friend tells the pet AND the user to stop).
- **Three-layer render** in bowl.md: pet line (from pet file) + bowl bar + narrator line (from voice.md pools), each pulled fresh.

### Changed

- **voice.md rebuilt into rotation pools** keyed by event and score tier (log confirms by entry size, recap opens by tier, overflow callouts, stash bury/dig-in, self-sabotage, close lines) to kill repetition.
- **Hard no-repeat rule**: never reuse a narrator line, pet sound, or action from the last ~3 turns this session.
- **Casual-wording pass**: looser, slangier, more contractions and shorter lines, while keeping proper sentence case. Pet's name now dropped in occasionally (~every 2nd-3rd message).

---

## [2.0.0] - 2026-06-02

### Changed (BREAKING: skill renamed)

- **Renamed `reverse-todo` to `kibble`.** New trigger `/kibble` (and "feed my pet"); legacy `/reverse-todo` and "I did [thing]" triggers still work as aliases.
- **Data dir moved** `~/reverse-todo` to `~/kibble`, with a symlink left at the old path so nothing breaks.
- **Notion database renamed** "Reverse To-Do List" to "Kibble" (same database_id, all history intact).

### Added (the Kibble flow)

- **The pet.** A dog or cat, named at setup, that is secretly the user. You feed it by logging. New onboarding flow (pick + name pet, forced first log). Stored in `config.json` `pet` block.
- **The bowl.** New `references/bowl.md`: a rendered bowl + pet reaction shown on every log and recap. Ten-segment fill toward 100, overflow past it. Low fill reads calm, never shameful.
- **Overflow tiers.** Recap/voice now shift emotionally past 100: 100-150 pure joy, 150-200 stuffed first soft flag, 200+ food-coma loving intervention (asks about the user, not output). Hard rule: past 200 never gamify the ceiling.
- **The squirrel stash.** New `~/kibble/stash.json` persistent surplus balance + ledger. Days over 100 bank the surplus at recap; brutal low days dig into reserves so a bad day reads as spending savings, not failure. Seeded with banked surplus from prior history (opening balance 1074).
- **No-future-tasks guard** made explicit ("that's a tomorrow thing").

---

## [1.2.0] - 2026-05-27

### Changed

- **Rebalanced the scoring rubric** for honesty. The previous rubric inflated low-end activities (brush teeth = 10, ~10% of a full day), which compressed the high end and let normal days drift past 100 too easily, weakening the over-100 brain-lying call-out. New rubric compresses small things into 1-15 and spreads big things into 36-100 so the spread reflects reality:
  - 1-5: Tiny but real (was 1-10)
  - 6-15: Normal small thing (was 11-25)
  - 16-35: Real lift (was 26-50)
  - 36-65: Heavy (was 51-75)
  - 66-100: Huge, defines the day (was 76-100)
- **ADHD executive function tax** dropped from `+5 to +15` additive to `+1 to +5` additive, proportional to the new compressed low end.
- **Recap tone tiers refined** for the new score distributions:
  - Under 30: very gentle (hard day, full stop)
  - 30-59: gentle, small day with real life in it
  - 60-99: warm, solid day
  - 100-149: blunt, the brain-lying call-out
  - 150+: louder, heavy day
- **Added a day-total milestones table** to `scoring.md` so what totals MEAN is explicit (Under 30 = hard, 60-100 = solid, 100 = full day anchor, 150-200 = heavy day, 200+ = "WTF go lie down").
- **Recalibrated all example numbers** in `scoring.md`, `voice.md`, and `SKILL.md` for internal consistency with the new rubric.

### Unchanged (intentionally)

- The anchor: **100 = a full day's worth of human output.** This is load-bearing for the brain-lying call-out, the recap tone shifts, and future burnout-baseline math. Moving it would break too much.
- Multipliers: bad-day (x1.5-2), invisible labor (x1.3-1.5), and first-time-in-a-while (x1.5) all preserved. These protect ADHD-validating scoring without warping the scale.
- All sync behavior, voice rules, categories, and modes unchanged.

### Migration note

Existing logs from v1.0-v1.1 keep their old scores. The skill does not retroactively rescore. New logs use the new rubric. If you want to compare across versions, the v1.0 day-total ~= v1.2 day-total x 0.7 in rough terms.

---

## [1.1.0] - 2026-05-27

### Added

- **Obsidian sync.** After every local write, the same file mirrors to `~/Documents/Obsidian Vault/Reverse To-Do/YYYY-MM-DD.md` with Obsidian-friendly frontmatter additions (`tags: [reverse-todo, daily-log]`, `cssclass: reverse-todo`). Reviews go to `reviews/` subfolder.
- **Notion sync.** One page per day in a "Reverse To-Do List" database. Properties: Name, Date, Total Score, Entry Count, 6 category numbers, Has Recap. Reviews go as child pages under the parent (not inside the day-database) titled "Week of YYYY-MM-DD" or "Month of YYYY-MM".
- **First-log Notion setup flow.** When `sync.notion.database_id` is null, the skill prompts the user to pick a parent page from their workspace, creates the database with the full schema, and persists the resulting IDs to `config.json` so it never has to ask again.
- **`sync` block in `config.json`** with per-target `enabled` toggles, vault path, and Notion IDs.
- **`references/sync-obsidian.md`** documenting the vault write rules and failure handling.
- **`references/sync-notion.md`** documenting the Notion MCP tool calls, property schema, and the search-and-upsert logic.
- **README.md** in the skill's voice, ADHD-focused, with the full how-to.
- **CHANGELOG.md** (this file).

### Changed

- **SKILL.md** now runs a Sync step after every local write in log, recap, and review modes. Local markdown is the source of truth; Obsidian and Notion are mirrors.
- Recap mode flips the Notion `Has Recap` checkbox to true on write.

### Notes

- **Failure handling:** if a sync target fails (vault missing, Notion offline, MCP not connected), the skill skips that target silently, mentions it ONCE in the next confirmation, and never blocks the local log. Local always writes. Local always wins.
- **Source of truth:** local markdown at `~/reverse-todo/YYYY/MM/YYYY-MM-DD.md` is canonical. Obsidian and Notion are write-only mirrors. If you want to edit, edit the local file (or any of the three) and re-run a log to re-sync everything.

---

## [1.0.0] - 2026-05-27

Initial release. ADHD-friendly reverse to-do list with 0-100 effort scoring and best-friend voice.

### Added

- **Three modes:** `log` (default), `recap`, `review` (week/month).
- **Six categories** designed to make ADHD brains feel seen instead of judged:
  - Small Tasks
  - Self-Care
  - Emotional Stuffs
  - Big Brain Hours
  - Creative Time
  - Rest (treated as output, not absence of output)
- **0-100 effort scoring per entry** with a rubric in `references/scoring.md`. 100 = a full day's worth of human output. Includes bad-day multiplier (x1.5-2), invisible labor multiplier (x1.3-1.5), ADHD executive function tax (+5 to +15), and first-time-in-a-while multiplier (x1.5).
- **Over-100 brain-lying call-out** in recap mode. When the total crosses 100, the recap explicitly tells the user their brain is about to try to discount it and not to let it.
- **Best-friend voice** codified in `references/voice.md`. Calls out self-sabotage, swears where it lands, bans productivity-bro language, treats rest as real work, names invisible labor explicitly.
- **Pattern-only reviews** in `references/review-template.md`. Surfaces specific day-of-week / category / score-trend patterns, skips generic stats.
- **Local markdown storage** at `~/reverse-todo/YYYY/MM/YYYY-MM-DD.md`. Plain text, greppable, portable.
- **Capitalization rules** added late on launch day after the user noticed all-lowercase entries. Voice is casual, not aesthetically lowercase. Proper sentence case everywhere.
- **No em-dashes, no en-dashes** as a hard rule across all output.

### Known limitations

- Single-day, single-user. No multi-day batch logging from a transcript yet.
- No manual score override in v1 (auto-only). Hybrid mode is on the roadmap if scores feel off.
- No body / cycle awareness tagging (intentionally deferred).
- No win archive / bad-day comparison / crash prediction yet (queued for v3 / v4).

---

[1.2.0]: #120---2026-05-27
[1.1.0]: #110---2026-05-27
[1.0.0]: #100---2026-05-27
