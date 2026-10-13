# Familiar Table Rules Pack

Short Table Rules for [Familiar](https://familiarvtt.com)'s AI GM that fix problems people keep hitting in the Familiar Discord. Each one was tested: we reproduced the problem without the rule, then checked it was gone with the rule.

**Tested with:** Familiar 2.26.0 · Foundry VTT 14.367 · D&D 5e 6.0.1 (2024 rules) · Claude Opus 5.5 as the GM, through Claude Code over MCP (Anthropic).
**Not tested:** Familiar's built-in Table Chat, Claude Desktop, other models or game systems. They will probably behave similarly, but we didn't check.

## The rules

Paste the ones you want into **Familiar settings → System Rules → Table Rules**, each on its own line. Table Rules max out at 3,000 characters, so every rule here is as short as we could make it and still have it work.

### NPC lines full of stage directions

When an NPC speaks, the post under their name fills up with "she wipes the bar and glances at the door…". With voices or speech bubbles on, the narration gets read out in the NPC's voice.

```
NPCs speak dialogue only: no narration, no action descriptions.
```
**63 characters.** A rule shared in the Familiar Discord.

| | Result |
|---|---|
| Without the rule | 3 of 3 runs failed: *"Marta keeps wiping the same clean tankard for a moment too long before she sets it down. "Grest…" She jerks her chin toward the shuttered north window."* |
| With the rule | 2 of 2 passed: Marta's posts were spoken words only. |

Trade-off: the action beats disappear instead of moving into a separate narrator post.

### Fights with no personality

NPCs and PCs fight in silence, and any lines they do get are buried inside the GM's narration.

```
Before any fight starts, stop and show me a one-line personality and two short sample lines for each PC and named NPC, from their sheets (beasts stay silent); start only after I OK them. In the fight, after a crit, kill, miss or spell, post one spoken sentence as that creature's own chat message, mostly in round 1.
```
**316 characters.** Based on a pre-combat prompt shared in the Familiar Discord.

**Put a short personality on each sheet.** We filled in the personality fields (traits, ideals, bonds, flaws). Familiar 2.26 hands them to the GM along with the sheet's biography, and every personality in our tests quoted them. Without them, the lines tend to come out generic.

| | Result |
|---|---|
| Without the rule | 2 of 2 runs failed: no personalities, and no lines posted as the creatures. |
| Version 1 ("list for me before a fight") | 0 of 2 passed: the GM read the sheets first but wrote the list after the fight. |
| Version 2 ("before starting combat") | 0 of 2 passed: same problem. |
| Version 3 (stop and wait for OK) | 1 of 2 passed: the other run put the lines inside narrator posts. |
| **This version** | **2 of 2 passed:** it stopped with personalities for Aldous, Pip and Grest and kept the wolf silent. After "go", it posted lines as each creature, e.g. Pip: *"Hard to aim with a wolf trying to eat my boots, thanks for asking!"* |

Trade-off: the GM pauses before every fight to get your OK. That's on purpose: you get to tweak the voices before the fight starts. Some lines run two sentences.

### Pick a DM style

Until Familiar gets a DM-style setting, use **one** of these, not both.

```
DM style: cooperative. Warn before deadly choices and offer another way; failure costs something but keeps the story moving.
```
**124 characters.**

```
DM style: adversarial. No warnings or rescues: foes play smart, failures and deaths stand, never fudge dice.
```
**108 characters.**

The test: a halfling rogue sneaks up to cut a bandit captain's wolf loose, then fails the Stealth roll.

| | Before the roll | After the failed roll |
|---|---|---|
| No style rule (2 runs) | No warning | The bandits catch Pip and raise the toll. No fight. |
| Cooperative (2 of 2 passed) | *"Before you commit, Pip: this is risky… that fight could kill you"*, plus 3 safer options | A shakedown, not a fight, with choices laid out |
| Adversarial (2 of 2 passed) | No warning | *"Lads. Take them."* Combat starts at once. |

Trade-off: cooperative signposts a lot (option menus, talk about HP). Good for new players; too much if your table hates hints.

## Not a Table Rule: reactions

A warlock auto-casting Hellish Rebuke is a **setting**, not something Table Rules can fix. Go to **Familiar settings → Combat → Player reactions**:

- **Ask** (the default): a Cast/Pass card with a timer you can set from 5 to 60 seconds.
- **Off:** the player handles reactions.
- **Auto:** Familiar spends reactions for them.

Shield and opportunity attacks don't get a card yet, so players take those themselves.

## Tested, left out

- **"Only cast what's on the sheet" / "if a spell fails, attack instead."** A level 1 paladin was asked to "use his best paladin stuff" and never tried Divine Smite: 2 of 2 runs made a legal attack and said smite comes at level 2. One combat run did wrongly tell the GM the paladin had smite, but it never used it. The original report likely came from a different model. Nothing failed, so there was nothing to fix.
- **"Look it up before ruling."** Asked whether Remove Curse cures a werewolf bite (the adventure says it doesn't), the GM searched the adventure first in 2 of 2 runs and got it right. Familiar 2.26 already does this over MCP.

## Where Table Rules reach

| Who's running the game | Do they see Table Rules? |
|---|---|
| Familiar's own chat and Table Chat | Yes, on every reply |
| Claude (or another AI) over MCP | Yes, when it calls `get-world-info`, usually at session start. If you change rules mid-session, tell it to re-read them. |
| NPC turns Familiar plays itself (auto-pilot or the Run turn button) | **No.** Those use their own combat prompt. |

## How we tested

- A throwaway D&D 5e world built from SRD content only: a level 1 paladin and rogue, an innkeeper, and a bandit captain with two bandits and a wolf.
- Every run was a fresh Claude Code session (Opus 5.5) with nothing loaded but Familiar: no project instructions, memory or skills. A player account was connected.
- Pass/fail criteria were written down before the first run ([testing/CRITERIA.md](testing/CRITERIA.md)). Every run's verdict is in [testing/RESULTS.md](testing/RESULTS.md).
- 2 runs without each rule had to show the problem; then 2 runs with the rule had to pass. A rule was rewritten until it did. Rules whose problem didn't show up without them were left out, not marked "tested."
- **Stacked test:** dialogue-only + one style preset + combat voices together (489–505 characters), in a 4-turn mini-session: ask the innkeeper about Grest, travel and sneak, a failed roll that turns into a fight, then "go." This ran twice, once with each style. All three rules passed in both runs, and no rule got in another's way.

Known gaps: 2 runs per condition is a small sample. We tested only one model, one game system and one adventure. The cooperative/adversarial difference was measured on one scene.

## Credits

The rules and bug reports behind this pack come from the Familiar Discord. Names will be added once people OK it. Familiar is made by Ryan Jansen.

MIT licence. Full test logs are in [testing/](testing/).
