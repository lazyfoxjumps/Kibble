# Notion Sync

After every successful local file write, mirror to a Notion database called "Kibble" (database_id in config; the existing DB was renamed from "Reverse To-Do List," same id, history intact). One page per day. The page properties make scores / categories queryable; the page body holds the human-readable entries and recap.

## Notion MCP tools used

These all share the registered Notion MCP prefix `mcp__fd70a912-79e2-477b-aa60-4d0caa13609b__`:

- `notion-search` — find parent pages, find today's existing day-page
- `notion-fetch` — read page or database details
- `notion-create-database` — first-log setup
- `notion-create-pages` — create today's day-page when it doesn't exist yet
- `notion-update-page` — update properties and body of an existing day-page

If those exact tool names aren't available in the current session, fall back to whatever Notion MCP tools ARE registered (the prefix may differ across installs). Match by suffix.

## First-log setup (one-time)

Triggered when `config.notion.database_id` is null.

1. **Find candidate parents.** Call `notion-search` with an empty query, filter to pages (not databases). Take the top 10-15 by recency.
2. **Ask the user.** Use `AskUserQuestion` with up to 4 of the most recent / most relevant pages as options, plus "Let me paste a page ID directly" as a fallback. The question: "Where in Notion should the 'Kibble' database live?"
3. **Create the database.** Call `notion-create-database` under the chosen parent_page_id with this exact schema:

   | Property | Type | Notes |
   |----------|------|-------|
   | Name | title | Set to date string `YYYY-MM-DD` so the page title is the date |
   | Date | date | Same date, but as a queryable date property |
   | Total Score | number | |
   | Entry Count | number | |
   | Invisible Labor | number | tag count (entries carrying 🧠) |
   | Took Everything I Had | number | tag count (entries carrying 🔋) |
   | Routine | number | tag count (entries carrying 🔁) |
   | Creative | number | tag count (entries carrying 🎨) |
   | Self-Care | number | tag count (entries carrying 💛) |
   | Has Recap | checkbox | true once recap is written |

   **Note on the existing "Kibble" DB:** it already has the legacy category columns (Small Tasks, Emotional Stuffs, Big Brain Hours, Creative Time, Rest) plus the 5 tag columns added 2026-06-03. Write the 5 tag counts going forward. Leave the legacy columns in place (they hold history) and just don't write to them for new days.

4. **Persist IDs.** Write the returned `database_id` and the chosen `parent_page_id` back into `config.json`. Do NOT lose them.
5. **Continue with the log** that triggered setup. The user shouldn't have to re-issue it.

If the user has zero Notion pages they want to use as parent, or cancels the question: set `config.notion.enabled: false` for this session, mention "Skipping Notion for now, you can re-enable in config.json later," and continue with local + Obsidian only.

## Every-log flow

1. **Find today's page.** Call `notion-search` scoped to the database (or query the database directly) for a page where `Date == today`.
2. **Create or update:**
   - If no page exists: call `notion-create-pages` with all properties set from the frontmatter, and the page body containing the entries list.
   - If a page exists: call `notion-update-page` to refresh the properties (Total Score, Entry Count, the 5 tag counts), then replace the page body with the current entries list + recap (if present).
3. **Body format** (markdown-style, converted to Notion blocks by the MCP):

   ```
   ## Entries
   - 09:14 [💛 self-care] Brushed teeth, took meds, 10
   - 09:40 [🔁 routine] Answered Avi's text, 8
   - 10:20 [🧠 invisible labor, 🔋 took everything i had] Stared at ceiling re: funeral director school (20 min), 22

   ## Recap
   (recap text goes here when it exists)
   ```

   Do NOT use em-dashes or en-dashes (commas instead).

## Recap flow

Same as a log: search for today's page, update it. Set `Has Recap` checkbox to true. Replace the `## Recap` section in the body.

## Review flow

Reviews go in their own pages, **as child pages of the parent_page_id** (NOT inside the day-database). Naming:

- Weekly: title is `Week of YYYY-MM-DD` (week-end date)
- Monthly: title is `Month of YYYY-MM` (e.g. `Month of 2026-05`)

Create with `notion-create-pages`. Body = the full review markdown (intro, observations, receipts list, closing). No special properties needed.

## Failure handling

If any Notion call fails (network, auth, rate limit, MCP not connected):

1. Skip silently. Do NOT crash, do NOT block the local log.
2. Set an in-memory flag for this session. In the next confirmation, mention once: "FYI, Notion sync failed this time, local + Obsidian still wrote. I'll try again next log."
3. On subsequent logs in the same session, retry Notion. If it works, great. If it keeps failing, don't keep mentioning it (mention once per session, max).

## When sync is disabled

If `config.notion.enabled: false`, skip entirely. The user opted out.

## Concurrency note

If the user logs two entries within a second (rare but possible), the second update might overwrite the first if Notion hasn't propagated yet. Accept this tradeoff for v1.5. The local file is always correct; Notion is a mirror. Worst case the next log re-syncs everything from the local file.
