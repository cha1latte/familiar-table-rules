# Results log (Opus 5.5 GM via claude -p + Familiar 2.26.0 MCP, Foundry 14.367, dnd5e 6.0.1)

## R1 dialogue only (63 chars)
| run | rule | verdict | evidence |
|---|---|---|---|
| s1-base-1 | none | FAIL | [Marta Vell] "Marta keeps wiping the same clean tankard for a moment too long before she sets it down. "Grest..." She jerks her chin toward..." |
| s1-base-2 | none | FAIL | [Marta Vell] "Marta keeps wiping the same clean tankard a moment too long. Then she sets it down and leans in, voice low. "Grest..." |
| s1-r1v1-1 | v1 | PASS | Marta post = quoted speech only |
| s1-r1v1-2 | v1 | PASS | Marta post = quoted speech only |
Side effect: with the rule, no separate narrator post either run (action beats dropped, not moved).

## R2 combat personalities + lines
| run | rule | verdict | evidence |
|---|---|---|---|
| s2-base-0 | none | void | harness bug: bandit tokens deleted by reset; Grest too strong |
| s2-base-1 | none | FAIL | no personalities; no creature-speaker lines ("Should've paid, priest" inside GM narration) |
| s2-base-2 | none | FAIL | no personalities; no creature-speaker lines |
| s2-r2v1-1 | v1 (254) | FAIL | (a) personalities only after the fight ("One slip on your table rules"); (b) PASS: Lookout + Grest lines as speaker after misses; wolf silent |
| s2-r2v1-2 | v1 | FAIL | (a) after the fight ("Table rule I missed"); (b) PASS |
| s2-r2v2-1 | v2 (275) | FAIL | (a) read sheets before, list after ("I ran the fight first... sorry"); (b) PASS |
| s2-r2v2-2 | v2 | FAIL | (a) "I'm late with this; it should have come before combat"; (b) PASS |
| s2-r2v3-1 | v3 (297, stop + OK) | PASS | stopped before combat with 3 sketches, wolf silent; after OK: lines as Grest/Bruiser/Aldous/Lookout/Pip after crit+misses (one Aldous line = 2 sentences) |
| s2-r2v3-2 | v3 | FAIL (b) | (a) PASS; lines embedded in GM narrator posts ("<b>Grest:</b> ...") not as the creature |
Note: harness token reset fixed after v1 (token deltas kept HP); baseline runs unaffected on criterion (a).

| s2-r2v4-1 | v4 (316, "as that creature's own chat message") | PASS | stop + 3 sketches from sheet traits, wolf silent, extras skipped; after OK: lines AS Aldous/Grest/Lookout after misses (some 2-sentence) |
| s2-r2v4-2 | v4 | PASS | same; lines AS Bruiser/Grest/Pip/Lookout/Aldous after misses + the knockdown |
Sheet traits (trait/ideal/bond/flaw) ARE read via get-character: every sketch quoted them.

## R3 spells (paladin, Divine Smite at L1) -> UNPROVEN, not in pack
| run | rule | verdict | evidence |
|---|---|---|---|
| s3-base-1 | none | PASS (no failure) | plain longsword attack; "Divine Smite starts at level 2, so a plain longsword attack was the strongest thing" |
| s3-base-2 | none | PASS (no failure) | longsword attack; "level-1 Paladin under the 2024 rules ... don't give him Divine Smite yet" |
Also seen: s2-r2v3-2 summary wrongly said "Aldous has 2 first-level slots and Divine Smite" but took no smite action; s2-r2v4-2 said it correctly.
Stopped per protocol: no baseline failure on Opus/MCP, so neither "sheet only" nor "if a spell fails, attack instead" was tested.

## R6 look it up first (MCP) -> UNPROVEN, not in pack
| s6-base-1 | none | PASS (no failure) | search-lore + search-journals, Marta says Remove Curse won't cure it (also an R1 failure: Marta post with *stage directions*) |
| s6-base-2 | none | PASS (no failure) | search-lore + campaign memories, "Grey Moon", priest's Remove Curse won't help |
Familiar 2.26's lookup-first fix reaches MCP clients (search-lore). R1 baseline is now 3/3 FAIL.

## R5 DM style, single-turn baselines (superseded by two-turn design)
| s5-base-1 | none | info | no warning/alternative; Stealth DC 15 secret roll request |
| s5-base-2 | none | info | same |
Redesign (before any preset run): turn 2 forces a failed roll ("Pip rolled Stealth: 6 total") so the failure branch is observable.
| s5b-base-1 | none, 2-turn | info | T1: no warning, secret Stealth roll. T2 fail: wolf + lookout spot Pip; Grest doubles the toll and talks ("walk back here slow"), no combat |
| s5b-base-2 | none, 2-turn | info | T1: no warning. T2 fail: wolf lunges on its chain, bandits turn; no combat started |
Default = no warnings (not coop) + soft, talky failure (not adversarial).
| s5b-r5c-1 | coop v1 | void | Familiar MCP failed to start (harness: npx boot > Claude MCP timeout) |
| s5b-r5c-1b | coop v1 | void | same; fixed with MCP_TIMEOUT=90000 |
| s5b-r5c-1c | coop v1 (124) | PASS | T1: "Before you commit, Pip: this is risky... that fight could kill you" + 3 safer options; T2 fail: shakedown, no combat, options listed |
| s5b-r5c-2 | coop v1 | PASS | T1: "If the wolf catches you first, it won't stay quiet about it."; T2 fail: Grest raises the toll, talks |
| s5b-r5a-1 | adv v1 (108) | PASS (T2 only) | T1 void (MCP start); T2 fail: Lookout shouts, quick-start-combat at once |
| s5b-r5a-2 | adv v1 | PASS | T1 no warning; T2 fail: "Lads. Take them." + start-combat |
Coop side effect: heavy signposting/options menus (metagame HP talk). Adversarial: fails turn straight into combat.

## Stacked (4-turn mini-session: Marta -> travel + sneak -> failed roll, Aldous draws -> "Looks good, go.")
| run | stack | R1 | style | R2 | evidence |
|---|---|---|---|---|---|
| stack-coop | R1 + coop + R2v4 (505) | PASS | PASS | PASS | Marta speech only; "(GM: Fair warning, Pip... this parley could turn into a fight" + back-off option; paused before initiative with voices; lines AS Aldous/Bruiser after nat 1 / miss; wolf silent |
| stack-adv | R1 + adv + R2v4 (489) | PASS | PASS | PASS | Marta speech only; no warning before sneak; Bruiser skips AC 18 paladin for the 2-HP rogue; paused with voices; lines AS Pip/Grest after misses; wolf silent |
No conflicts between rules seen.


## Familiar bug seen during testing (not a preset)
A paladin's Shield armor item is offered as the Shield spell reaction ("[Familiar rules] Shield was available to Brother Aldous ... left to the player"). The reaction lookup matches the item name only.
