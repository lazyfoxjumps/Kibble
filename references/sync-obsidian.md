# Obsidian Sync

After every successful local file write (log, recap, or review), mirror to the user's Obsidian vault.

## Where it writes

Path: `<vault_path>/<subfolder>/YYYY-MM-DD.md`

With defaults from `config.json`, that resolves to:
`~/Documents/Obsidian Vault/Reverse To-Do/2026-05-27.md`

Tilde-expand `vault_path` at runtime. Create `<subfolder>/` if it doesn't exist.

For reviews: `<vault_path>/<subfolder>/reviews/YYYY-MM-DD-week.md` (or `-month.md`).

## What's different from the local file

Mostly nothing. Same body, same entries, same recap. Two small additions to the frontmatter for Obsidian-friendliness:

```yaml
---
date: 2026-05-27
entries: 3
total_score: 40
categories: { small_tasks: 8, self_care: 10, emotional_stuffs: 0, big_brain_hours: 22, creative_time: 0, rest: 0 }
tags: [reverse-todo, daily-log]
cssclass: reverse-todo
---
```

`tags` and `cssclass` are Obsidian-native. The user can build dashboards, dataview queries, or theme overrides around them later without us doing anything.

For review files use `tags: [reverse-todo, review, weekly]` (or `monthly`).

## Sync rule

Sync is **last-write-wins** and **always full file**. Don't try to diff or patch. Read the freshly-written local file, add the Obsidian frontmatter additions, write the whole thing to the vault path. This keeps the two files identical and avoids drift.

## Failure handling

If the vault path doesn't exist (user renamed it, vault unmounted, drive disconnected):

1. Skip silently. Do NOT crash, do NOT block the local log.
2. Set a flag in memory for this session so we mention it once in the next confirmation: "FYI, couldn't reach your Obsidian vault, local + Notion still wrote."
3. Don't nag on every subsequent log in the same session.

If creating the subfolder fails (permissions, disk full): same behavior. Skip + mention once.

## When sync is disabled

If `config.json` has `sync.obsidian.enabled: false`, skip entirely. No mention, no warning. The user opted out.
