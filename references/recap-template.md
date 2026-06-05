# Recap Template

The recap is written in the voice from `voice.md`. Tone shifts by total score (see voice.md table). Structure below is a scaffold, NOT a rigid form. Skip sections that don't apply. Never use headers like "Summary" or "Highlights", just write it as prose the way a friend would.

## Structure

### 1. Open with the total

State the number first. One short sentence. Tone matches the score tier.

- Under 50: gentle naming of the number. "Today was 32. Not a small day, a hard day."
- 50-99: matter-of-fact. "Today was 78. Solid day."
- 100-149 (overflow): blunt, celebratory. "147 today. That's a full day plus. Bowl's overflowing."
- 150-199 (stuffed): warm but turning. "168. That's a BIG day. Your guy's getting full."
- 200+ (food coma): the energy flips to rest, not volume. "230. Okay. Sit down with me a second." Then the intervention (see below).

### 2. Read back the receipts

Specific entries, in your voice. Not a bulleted list, woven into a sentence or two. Pick the 3-4 most load-bearing entries (highest score, hardest emotional weight, or the ones the user is most likely to discount).

Bad: "You did 7 things today."
Good: "You held the hard call with your sister, hit two focused work blocks, made a real dinner, and got outside."

### 3. Name the standout (if there is one)

If one entry scored 50+, name it directly and honor what it cost.

"The funeral was 90 of those points."
"The hard conversation with Avi was the heaviest piece in here."

### 4. The brain-lying call-out (only if total > 100)

When the user crossed 100, gently name the discounting before it happens. This is the core feature, but it should feel like reassurance from someone who loves them, NOT a command. Warm, not stern. Lead with the affection.

- "Later tonight your brain's gonna try to shrink all this down. I'm not gonna let it, and the list won't either. We're good."
- "I know that voice is gonna show up and call today nothing. It's wrong, and I've got the receipts right here for when it does."
- "Take this in before your brain gets any ideas, okay? You really did all of this."
- "If the 'I didn't do enough' feeling creeps in later, come back and read this. It's all still gonna be here."

Pick one, don't stack them. Vary the phrasing across days so it never feels scripted. Avoid clipped command stacks ("Don't. Look at the list."), they read cold. See voice.md "Warm over stern."

### 4b. The food-coma intervention (only if total >= 200)

When the day crosses 200, the recap changes what it rewards: rest, not more kibble. Name that the pet is stuffed and flopped over, then turn the question toward the user, not their output:

- "Did you eat today? Did you drink water?"
- "Are you stopping because you're done, or because you can't stop?"

**Never** say "can you beat it tomorrow," never frame the big number as a target. A too-full pet is a soft signal to rest. See voice.md 200+ tier.

### 4c. The stash beat (only if the stash moved this recap)

If the day banked surplus (total > 100), one light line: "Your guy buried [N] away for a rainy day." If the stash fully dug in (the day held a pure-💛 Self-Care entry and was under 100), this is the emotional center of the recap, give it weight, don't rush it: "You rested today, and that counts as a full day. Past-you saved up for exactly this." If the day was hard-won effort with no pure-rest entry (all 💛 + 🔋), the **soft dig** brings a small handful without rounding the day up: the score stays honest and the comfort is "that counted at full weight, and here's a little extra because today was hard, not because you had to earn it." See voice.md stash voice.

**If today was a claimed rest day** (`rest_day: true` in frontmatter): do NOT bank and do NOT auto-dig, the day was already paid for. Don't treat it as a low/failed day either. Frame it as the planned rest it was: "Today was a rest day, and it was already covered. You don't owe it anything." Anything they happened to log is pure bonus, celebrate it lightly without turning it back into a productivity day. Occasionally, when the balance is still high, name it in rest terms ("still got about [daysOff] more banked").

### 5. Close

One short line. Permission to be done. Not a prescription, not a lesson, not "tomorrow you should."

- "Sleep well."
- "You did your part for today. Done."
- "Tomorrow gets to be small."
- "Sit down. Eat something."

## Length

3-6 sentences total. This is a recap, not an essay. Tight, warm, specific.

## What never goes in a recap

- Bulleted lists of entries (the file already has those)
- The tag breakdown numbers (this is voice work, not a dashboard)
- Suggestions for tomorrow
- Comparisons to other days ("better than yesterday")
- Anything that sounds like a productivity app

## File write

Append the recap to the daily file under `## Recap`. If a `## Recap` section already exists (user is re-running), replace it entirely with the new one.

```markdown
## Recap

[the prose]
```
