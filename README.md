# Kibble 🐶🐱

**A reverse to-do list with a pet that's secretly you.**

You don't log what you have to do. You log what you already did, then you feed a little guy who is, plot twist, you. The version of you you'd actually be nice to.

> 🐶 *woof!* \
> 🐱 mrrp?

---

## The pitch, in one breath

Regular to-do lists are a war crime against the ADHD nervous system. You stare at a wall of unfinished stuff, your brain reads it as "I'm a failure," and now you're frozen in front of the thing that was supposed to help. Cool. Real productive.

Kibble flips it. Every single thing you did today, even brushing your teeth on a day that tried to flatten you, drops **kibble** in your pet's bowl. The kibble is your effort score, 0 to 100, where 100 is a full day of being a human with a body and feelings. Your pet gets rounder and happier as the day goes. You can't starve it. You can't fail it. You feed it by living.

So when your brain swears at 9pm that you "did nothing," you pull up the bowl, it's overflowing at 147, and now your brain has to argue with a stuffed, blissed-out animal instead of with you. The animal wins. The animal always wins.

**Kibble celebrates the big day, but it's secretly rooting for you to not need one.**

---

## Meet your guy

Pick a **dog** or a **cat** and name it. Naming matters, people are kinder to named things. First thing it ever does is make you log one win so the bowl reacts before you've even committed. That's the hook, and yeah, it works.

- 🐶 **The dog:** loud, loyal, zero chill, leans his whole weight on you, thinks you're the greatest person alive for the crime of existing. *AROOOO.*
- 🐱 **The cat:** acts like she tolerates you, then headbutts your hand the second you log something. The affection is real, it just arrives sideways. *slow blink.*

The pet doesn't talk. It woofs, it meows, it `*flops belly-up*`, and a best friend stands next to the bowl narrating, hyping you up, and occasionally telling the pet to sit down and chew its food.

---

## The bowl

Fills as the day adds up. Low is calm, never shameful, a nibble is still a nibble. Cross 100 and it overflows, and the pet does a full happy-dance.

```
🐶 Biscuit: WOOF *play bow*
🍚🍚🍚🍚🍚🍚░░░░  60 / 100
Oh that one took some juice. Scooping Biscuit extra for it. +25.
```

## What happens past 100

The pet's reaction isn't linear. The vibe quietly turns from "go" to "okay, sit down":

- **100 to 150, pure joy.** Bowl spills over, biggest happy-dance. You earned the party. 🐶 *victory laps*
- **150 to 200, stuffed.** Round belly, slowing down. "You're allowed to stop, you know." 🐱 *loafs hard*
- **200+, food coma.** The pet flops tummy-up and the prize stops being more kibble. It becomes rest. Kibble asks about *you*, not your output: did you eat, did you drink water, are you stopping because you're done or because you can't stop? It will **never** ask you to beat it tomorrow.

## The stash 🐿️

Anything over 100 gets buried away like a squirrel with acorns. A 220 day banks 120. Then on a brutal low day, when you scrape together 15 and your brain starts the spiral, the pet digs up the reserves and tops the bowl anyway:

> 🐱 Goblin: *fishes the hidden stash back out, drops it in the bowl for you* \
> "Rough one, huh. That's fine. Past-you saved up for exactly this. You're covered."

Big days protect bad days. A bad day stops being a failure and starts being savings you already earned.

---

## The 5 tags

Each entry gets zero or more (multi-select). Two of them stack on top of anything.

- 🧠 **Invisible Labor** — the work nobody sees but you. Hard convos, mental load, masking, boundaries, the deep thinking. The most discounted stuff there is.
- 🔋 **Took Everything I Had** — not an activity, an intensity flag. Stack it on anything that cost you way more than it "should have." This is what lets leaving the house on a depression day score high.
- 🔁 **Routine** — errands, chores, bills, replies, the upkeep.
- 🎨 **Creative** — you made a thing that didn't exist before. Good or not, shipped or not.
- 💛 **Self-Care** — food, meds, hygiene, movement, therapy, and rest. Rest is output, not the absence of it.

---

## The three modes

**`log`** (the default). Tell it what you did. It tags, auto-scores, drops the kibble, shows the bowl. You never invent the number, that's the whole point, the ND brain doesn't get to stall scoring its own worth.

**`recap`.** End of day. Reads your wins back, totals the bowl, banks or digs into the stash, and tucks the little guy in. The tone shifts with the number, all the way up through the food-coma intervention.

**`review`.** Weekly or monthly pattern-spotting. Not generic stats. Stuff like:

> "Your Mondays spike to 130 and Tuesdays crater to 41. You're cooking yourself Monday and crashing the next day."

> "60% of your week carried the 🧠 Invisible Labor tag. You're the designated feelings-holder for someone right now. That's real, and it's expensive."

---

## Where your data lives

1. **Local markdown** at `~/kibble/YYYY/MM/YYYY-MM-DD.md`. The source of truth. Plain text, greppable, yours. (The old `~/reverse-todo` path still works, it symlinks here.)
2. **Stash** at `~/kibble/stash.json`, the running surplus. Local only.
3. **Obsidian** (optional sync), same daily files with tags.
4. **Notion**, a database called "Kibble," one page per day, fully queryable.

Local always wins. If Obsidian or Notion is down, you still log. Nothing here is fragile.

---

## Install

```bash
# 1. Clone into your Claude Code skills folder
git clone https://github.com/lazyfoxjumps/kibble.git ~/.claude/skills/kibble

# 2. Copy the example config
cp ~/.claude/skills/kibble/config.example.json ~/.claude/skills/kibble/config.json
```

Then open `config.json` and tweak:
- `log_dir` if you want logs somewhere other than `~/kibble`
- `sync.obsidian.vault_path` to point at your vault (or `enabled: false` to skip)
- `sync.notion.enabled: false` if you don't use Notion. If you do, leave the IDs null and it'll set itself up on your first log.

Connect the Notion MCP if you want Notion sync. Obsidian needs nothing, it's just file writes.

---

## How to use it

Just talk to it. Anything that sounds like "here's what I did" logs:

- `/kibble brushed teeth and ate lunch`
- `feed my pet: paid 2 bills, answered 3 emails, made a real dinner`
- `I just got off a hard call with my mom`

Or the explicit moves:
- `/kibble recap` at end of day
- `/kibble review week` / `/kibble review month`

The legacy `/reverse-todo ...` triggers still work. And if you spiral, just say "I didn't do anything today" and watch it pull up the bowl and read it back at you. That's the entire point.

---

## What Kibble will never do

- Lecture you, or tell you what you "should" do tomorrow
- Use "grind," "hustle," "crush it," or chase a high score (past 200 it actively tells you to stop)
- Pretend rest doesn't count
- Compare you to anyone, or to your own best day
- Punish a missed day (the pet just naps, no streak resets)
- Be mean to the pet (it's secretly you, so that'd be mean to you)
- Use em-dashes (banned forever, on principle)

What it WILL do is keep the receipts, feed the little guy, and hand the receipts back when your brain rewrites history. That's the gig.

---

## Files

```
kibble/
  SKILL.md              the 3-mode dispatch, pet, stash, onboarding
  config.json           paths, pet, stash, sync settings, tags
  config.example.json   template config
  README.md             this thing
  CHANGELOG.md          version history
  references/
    categories.md       the 5 tags and what counts in each
    scoring.md          the 0-100 rubric with anchor examples
    voice.md            the voice: pools, warmth rules, what's banned
    bowl.md             the bowl + pet render and overflow states
    pet-dog.md          the dog's sounds, actions, and personality
    pet-cat.md          the cat's sounds, actions, and personality
    recap-template.md   end-of-day report structure
    review-template.md  weekly / monthly rollup structure
    sync-obsidian.md    Obsidian write rules
    sync-notion.md      Notion schema + setup flow
```

---

## A note on the voice

Kibble talks like a best friend who's known you for years and happens to be holding a bowl. Warm, funny, casual, never stern, never snarky. It swears when it lands. It calls out the brain-lie but never you. The pet is the warmth, the receipts are the honesty.

Don't like the voice? It lives in `references/voice.md` and is the most editable part of the whole thing. Make it sound like whoever YOU need on a bad day.

---

## Why this exists

ADHD brains delete wins instantly. Mine does it too. I needed something that holds the receipts so my brain has something to argue with at 9pm. Turning it into feeding a little guy who's secretly me made it the rare thing I'd actually open. Maybe it does that for you too.

If your brain is mean to you, this might be the friend you keep on your machine.

> 🐶 *woof.* (he agrees) \
> 🐱 *slow blink.* (so does she)
