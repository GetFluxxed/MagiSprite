# MagiSprite — proposed game design

## 0. A proposal to test

Version 0.2 · Updated after visual review. **MagiSprite** is the repository name. *The Living Atlas* remains a proposed creative theme/title; names, fiction, values, and systems are **proposals**, except the owner-selected combat direction and explicit requirements in [ARCHITECTURE.md](ARCHITECTURE.md). See [ART_DIRECTION.md](ART_DIRECTION.md) for the approved combat reference and proposed animation specification. No playable implementation or completed animation clips are included.

**Pitch:** A Sprite Mage journeys into places the world has forgotten, bonds with the creatures that remember them, and carries their stories home in a growing field dossier. Every expedition builds a new team; every return leaves a more capable Mage and a richer Book.

The distinctive pleasure is choosing **what kind of naturalist to become during this run**. Taking the safer river route may strengthen Water affinity, letting you bond a rare river guardian; following the fading stars may open Space affinity but leave your current party underfed. The Book teaches how to make those choices. It is a useful account of lived encounters, not a catalogue of locked silhouettes.

| Design pillar | Concrete consequence | Risk to test |
|---|---|---|
| Collect through understanding | Visible bond requirements and enemy intent; knowledge reduces uncertainty | Too predictable once solved |
| A fresh expedition, a lasting record | Bonds and equipment reset; Mage XP and discoveries survive | Players may expect permanent creature ownership |
| Individual turns, little waiting | Three active Sprites, clear target previews, short effects, no decision timer | Actions may feel too similar |
| Stronger possibilities, not endless inflation | Small Mage tree, finite elite tiers, meaningful specialist penalties | Meta progression may feel too slight |
| A book worth opening | Dossiers include habitats, bond thresholds, observed actions, and variants | Excess reading can interrupt pace |

These are original design proposals. The owner's named games are references for collection, party turns, unlockable archetypes, food progression, and pixel atmosphere, not instructions to reproduce characters, worlds, branding, or interface assets.

## 1. Scope and the first playable slice

Target a landscape phone experience with three active Sprites and one reserve. The Mage travels visibly with the party but has no HP or independent turn. Its affinities, passive, and one support command shape the team. This keeps U29–U30's individual Sprite turns while limiting four-actor menu overhead. Portrait orientation remains a deliberate alternate to test.

Proposed eventual run: **12–18 minutes**, three regions of four selected nodes each, one regional guardian in each region. Each four-node segment contains two encounter slots, one choice slot (camp, event, or trader), and a guardian. One of the two encounter slots can be an optional elite. Branches choose habitat and reward, but reconverge before the guardian. Region 3's guardian ends the run. This produces nine fights and three noncombat stops. Targets: ordinary fight 35–60 seconds, guardian 90–120 seconds, and 2–4 minutes total for routing, rewards, and reading. These are hypotheses, not measured performance.

**Initial test slice:** one region, one guardian, two Mage sheets (Wayfarer and Kilnkeeper), six common-habitat Sprites, three rare-element Sprites represented in scripted encounters, twelve item definitions, one elite variant, and five Mage-tree nodes. Paper tests precede any code. A later approved prototype can reuse the same specification.

Out of this slice: PvP, real-time fighting, multiplayer, breeding, fusion, permanent creature storage, procedural narrative generation, online leaderboards, live operations, monetization, accounts, cloud saves, and an engine decision. The package does not establish these as permanent exclusions.

## 2. The expedition loop

1. **Prepare in the Waystation.** Choose a Mage, spend/refund Mage-specific points, review discovered pages, select one known common starter, and allocate two temporary affinity points. First expedition offers Cindermoth only; the tutorial's first encounter introduces a second element.
2. **Read the route.** Each branch shows habitat, encounter category, and its guaranteed affinity reward. Species identities remain hidden until encountered. A reachable rare habitat can be seen before committing to it.
3. **Explore a small scene.** Tap a node or a visible interaction to walk there automatically. No virtual joystick, reflex hazards, or repetitive random battles. Idle means ambient animation while waiting for input, with no offline income or timed loss.
4. **Fight or bond.** Read intent, choose each Sprite's action and target, and decide whether to spend a bond charge. A bond can change the party immediately after combat.
5. **Resolve one reward panel.** Grant encounter coins and XP, reveal one rarity-selected item, and choose one of two advertised affinity increases. Food can be assigned here or saved. The panel also announces a new dossier without forcing it open.
6. **Make a recovery decision.** At a camp, choose party healing (35% maximum HP each, reviving downed Sprites at that amount) or one bond charge; no free full reset. A trader sells a small fixed stock at listed prices.
7. **Face the guardian.** Its intent requires using the team rather than merely matching an element. The final guardian offers a short story reveal and the run summary.
8. **Return with evidence.** Show one page update, Mage XP, unlocked choices, and the run's depth/score. The replay button is available after the summary; no streak or countdown pressure.

**Failure/retreat:** a wipe occurs when all three active Sprites are down and there is no living reserve. If the active team is down and a living reserve exists, it enters the first slot before the next turn. An ordinary fight permits retreat to the Waystation at the next player decision; guardian retreat is also allowed but ends the run. Previously earned XP, unlocks, and Book entries survive; the uncompleted encounter grants nothing. Quitting the app suspends rather than forfeits the run.

For a later implementation, save after every committed action/reward and before presenting a new decision. Resume restores the same state and pending reward; it must not generate a new roll. This is a behavior contract, not a selected persistence technology.

**Local score proposal:** 100 per completed region + 10 per completed fight + 15 per distinct species bonded in that run (excluding the starter) + 25 per optional elite victory. Record Mage and Mage level beside the score; no speed bonus, so reading and accessibility settings carry no penalty. Count each resolved encounter once. Best depth remains a separate record; online comparison is outside the slice.

## 3. Combat: fast decisions, readable consequences

### Turn model and resources

Each living actor acts once per round. At round start, sort by Speed, descending; ties favor player actors, then stable party/enemy slot order. Show the complete current-round queue. Speed changes affect the next round only. A newly substituted reserve occupies the outgoing actor's slot next round and does not gain an immediate extra turn.

Each Sprite has HP, Power, Guard, Speed, and Focus. Focus starts at 3 each encounter, caps at 5, and is individual. **Strike** costs 0 and grants 1 Focus after resolving. **Guard** costs 0, grants 1 Focus, and reduces the next damaging hit before the Sprite's next turn by 50%. A Sprite has two signature skills, usually costing 2 and 3 Focus, plus a neutral Strike. No random misses or critical hits in the slice. Skill elements, resource costs, target rules, and expected damage are visible before confirmation.

One action per Sprite turn: Strike, signature skill, Guard, Bag item, Bond, Swap, or **Conduit**. Conduit spends that Sprite's turn to invoke the Mage's once-per-encounter support command. Any eligible Sprite may invoke it; it cannot be used again that encounter. This keeps Mage involvement explicit without adding a fourth individual combat turn. Bag items spend the acting Sprite's turn and one item; items cannot target an ineligible/full-HP target. Bond and swap have the rules below.

**Damage proposal:** `max(1, floor((Power × move potency − target Guard × 0.5) × element × guard factor))`. Potency is 1.0 for Strike, commonly 1.4 for an offensive skill. Guard factor is 0.5 while Guard is active, otherwise 1.0. Apply listed shields after this calculation; a shield may reduce the resulting HP loss to 0. Avoid unlisted random variance. Status ticks ignore Guard and element, and follow their own fixed rule.

Example: Cindermoth Power 20 uses Flare (potency 1.4, Fire) on Grass Brambleback, Guard 8. Before defense buffs, `(28 − 4) × 1.5 = 36` damage. Guarded target: 18. Neutral Strike against that same unguarded target: `20 − 4 = 16`. These numbers are examples for the paper test, not balance findings.

### Three statuses and one team mechanic

| Status | Proposed rule | UI |
|---|---|---|
| Scorch | Lose 4 HP at the end of own turn, for 2 turns; reapplication refreshes, does not stack | Flame + number of ticks |
| Root | Speed −3 for the next round only; does not remove a turn | Root + next-round icon |
| Ward | Absorb the next 8 incoming damage; excess passes through; ends with encounter | Shield + remaining amount |

**Resonance** gives team composition a payoff without a separate action-bar system. An effective elemental hit adds one shared pip (maximum 3, at most one per action). At three pips, the next successful player signature skill consumes all three and grants all living allies Ward 8 after its effects resolve. That consuming action does not also generate a pip. Pips reset between encounters. Healing/support skills can consume but cannot generate pips. The visible shared meter explains both rules.

This creates a reason to sequence weakness hits before a support skill. It may be unnecessary complexity: test the game without Resonance first, then retain it only if players can explain and deliberately use it.

### Example round and encounter design

The enemy Brambleback announces “Thorn sweep · all allies · next turn.” Cindermoth's turn previews Flare for 36 damage, enough to remove it; alternatively, Guarding lets Dewseal spend its later turn on a needed heal. A wounded second enemy can be bonded instead of finished, but Bond uses a turn and the last charge. There is no hidden capture percentage to encourage repeated tapping.

Ordinary encounters teach one relation or status; mixed-element pairs force target selection; elites add a visible drawback; guardians change intent at half HP. Prototype guardian **The Unwritten Stag** alternates a single-target attack and a telegraphed party sweep. Guard/ward is always a viable answer even without a favorable element. Its Sprite Book entry is earned on defeat, but its Bond button says “Guardian · cannot bond in this chapter.”

### Interaction and pacing

Tap action → tap target → view exact outcome preview → confirm. A quick-confirm preference may combine target and confirm after onboarding; default does not. Back cancels before commitment. Make unavailable actions inspectable and state the specific reason (“Fire affinity 1 / 2,” “Need 2 Focus,” or “No bond charges”). Enemy-target buttons are available in addition to tapping pixel characters.

Keep routine impact effects around 250–450 ms and the total action presentation under 0.8 seconds at normal speed. A 2× setting accelerates animation only. Freeze decisions while backgrounded; do not require fast taps to succeed. Reduced motion removes shake, flashes, and parallax. Touch targets are proposed at least 48 logical pixels, body labels at least 16–18, with text enlargement and shape/name redundancy for element and rarity colors. Actual touch comfort and contrast must be measured in a later interactive prototype.

## 4. Affinities, bonding, and Mage identity

### Current stats determine access (U13)

Track six **Mage affinity stats** independently from Sprite combat stats. The Wayfarer begins each run at Fire 2, Grass 2, Water 2, Void 1, Space 1, Prismatic 1; allocate two additional temporary points before departing. Each completed fight grants a choice of +1 to one of two affinities advertised on that route. Each affinity caps at 6. Temporary route bonuses are part of current stats and reset between runs.

Normal common-habitat Sprites require affinity 2; their elite variant requires 3. Void, Space, and Prismatic Sprites require their affinity 4. Special species may eventually have secondary requirements, but the slice uses one requirement per Sprite. Baseline Wayfarer can reach every element, including the three rare elements, within a run. Optional specialist penalties are visible before departure.

Bond requires all of: target is bondable, target HP is at or below 30% maximum, relevant current affinity meets its threshold, and at least one bond charge remains. When those conditions are satisfied, Bond **succeeds deterministically**, spends one charge and one Sprite turn, and removes the target peacefully. Intent plus the HP preview helps avoid accidentally defeating it. A successful bond consumes the encounter's target exactly once; defeating, bonding, and release must never multiply rewards.

Start with 2 charges, cap at 3; camps and one item restore charges. At full party capacity, the post-combat panel compares the new Sprite against the reserve and allows replacement or release. The bond still counts for research even if released; the starting Sprite, swaps, and releases never count as new bonds. New recruits cannot act in the current fight. Bonding all enemies counts as clearing the encounter and gives the same base reward as defeating them.

### Proposed Mage roster

| Mage | Role and support command | Affinity/benefit | Explicit cost | Unlock |
|---|---|---|---|---|
| **Wayfarer** | Adaptable field naturalist; Conduit grants Ward 8 to living allies | Baseline stats above; +2 freely allocated points | No penalty; no specialized offensive bonus | Default |
| **Kilnkeeper** | Burn-focused; Conduit applies Scorch to all enemies | Start Fire 4, Grass 2, Water 1, rare affinities 1; +2 allocation points | Water food grants 25% less XP, calculated after food match; disclosed rounding down | Finish a region with two Fire Sprites alive |
| **Tide Listener** | Recovery; Conduit heals living allies 12 HP | Water 4, Grass 2, Fire 1, rare affinities 1; +2 allocation | Fire signature moves cost +1 Focus | Later proposal: win a guardian fight without a Sprite going down |

Only the first two Mage sheets are in the initial slice. Do not develop all archetypes before the basic Mage is enjoyable. Unlocks must allow natural play, must remain earned after a failed run, and must never require paid randomness.

## 5. Elements and the first bestiary

Proposal: finish the main cycle as Fire > Grass > Water > Fire. Effective hits are ×1.5; the reverse directions are ×0.75. Void and Space are ×1.5 against each other, otherwise neutral. Same-element hits are neutral. **Rows are move types, columns are defending Sprite types.**

| Attack ↓ / target → | Fire | Grass | Water | Void | Space | Prismatic |
|---|---:|---:|---:|---:|---:|---:|
| Fire | 1 | 1.5 | .75 | 1 | 1 | 1 |
| Grass | .75 | 1 | 1.5 | 1 | 1 | 1 |
| Water | 1.5 | .75 | 1 | 1 | 1 | 1 |
| Void | 1 | 1 | 1 | 1 | 1.5 | 1 |
| Space | 1 | 1 | 1 | 1.5 | 1 | 1 |
| Prismatic | 1 | 1 | 1 | 1 | 1 | 1 |

Prismatic Sprites can provisionally learn one selected move from any element between encounters, replacing one signature slot. **When a Prismatic Sprite uses a learned move, its damage becomes Prismatic**; the move's utility remains, and the conversion is printed on the card. This preserves “no default strength or weakness” and prevents a universally optimal type. Prismatic is immune to neither statuses nor damage. This interpretation needs owner approval; the alternative is typed learned attacks, which would make offensive neutrality untrue.

| Sprite | Element / role | Two proposed signature skills (cost) | Visual hook | Bond affinity |
|---|---|---|---|---:|
| Cindermoth | Fire / striker | Flare: 1.4 potency Fire (2); Soot Wing: Scorch one enemy (2) | Charred map wings, lantern abdomen | 2 |
| Kilnling | Fire / protector | Stoke: Ward self + ally (2); Furnace Tap: 1.4 Fire (2) | A walking fired-clay seed oven | 2 |
| Brambleback | Grass / defender | Tangle: Root one enemy (2); Thorn Lash: 1.4 Grass (2) | Seed-shell armadillo with bramble ribs | 2 |
| Fernwhisk | Grass / enabler | Sap Sip: heal one ally 12 (2); Reed Cut: 1.4 Grass (2) | Fern fronds shaped into listening ears | 2 |
| Dewseal | Water / healer | Dew Mend: heal one ally 12 (2); Tidal Push: 1.4 Water (2) | Droplet-shaped seal with lily collar | 2 |
| Rillfin | Water / quick striker | Jet: 1.4 Water (2); Ripple: Ward one ally and self (2) | Folding fish made of moving stream ribbons | 2 |
| Hollowbell | Void / disruptor | Quiet Toll: remove target Ward, then 1.0 Void (3); Hush: Root (2) | A hollow bell with a living shadow | 4 |
| Orbitail | Space / support | Comet: 1.4 Space (2); Star Shelter: Ward all living allies (3) | Small nocturnal creature with a ringed tail | 4 |
| Prismfold | Prismatic / adapter | Facet: 1.4 Prismatic (2); Borrowed Gesture: selected learned move at its listed cost | An origami creature that refracts its surroundings | 4 |

For paper sessions, level-1 common Sprites start at HP 60, Power 20, Guard 8, Speed 8, except roles: striker Power +2 / Guard −2; defender HP +12 / Speed −2; healer Guard +2 / Power −2; quick striker Speed +3 / HP −6. These are one-time role changes, not per-level multipliers. Rare-element Sprites start with the common base; their unusual utility is the reward. Apply the same formula to enemies unless an encounter sheet explicitly says otherwise.

**Encounter availability is separate from item rarity.** Provisional unrestricted species-slot distribution is Fire 32%, Grass 32%, Water 30%, Void 2.5%, Space 2.5%, Prismatic 1%. Within an element, choose uniformly among eligible species, then variant. Habitat-specific tables explicitly replace those weights, so these numbers are not claimed as final run-wide rates. Never roll a rare species in a habitat whose reachable affinity rewards make it impossible to bond by that point; provide a scheduled rare habitat later rather than secretly replacing an encountered Sprite. In the paper slice, script rare encounters to test their rules; do not claim scripted frequency proves discovery pacing.

## 6. The Sprite Book: knowledge as the collection

The Book begins with **no species pages**. The tutorial's starter bond creates the first page but gives no repeat-bond research credit. After an encountered Sprite is defeated or bonded, insert a page for that species. Merely seeing it and retreating does not add a species page. The route journal can mention a strange sighting without creating a hidden catalogue slot.

| Record state | What is visible | Trigger |
|---|---|---|
| Absent | No page, no question-mark entry, no empty numbered slot | Never defeated/bonded |
| Recorded | Sketch, element, habitat observed, observed actions, readable bond requirements | First defeat or bond |
| Bonded | Full skillset, role notes, bond count | First bond |
| Studied | Elite research note and next-run eligibility | Third nonstarter bond of that species |

Use discovery-order folio numbers, not global bestiary numbers, so the UI does not expose missing species. Display “7 discovered,” never “7 / 99” before the owner decides otherwise. Filters contain only discovered types. Reading is always optional; reward notices can open the relevant page directly.

An entry contains: name, illustration, element with shape label, role, observed habitat, bond requirements with current-run comparison, observed combat notes, total defeats, successful research bonds, learned lore fragments, and known variant tabs. Unknown information within an existing page may be marked “Not yet observed”; it must not manufacture an entirely new undiscovered species page.

**Elite research proposal (U09):** at 3 research bonds, unlock one elite variant for subsequent runs. For future eligible occurrences of that species, 10% become elite; the remaining 90% stay normal. Species encounter weights and item rarity probabilities do not change. Elite has +20% Power, −20% Speed (round down, minimum 1), a visibly different silhouette, and bond affinity 3 for common species. No elite tiers for rare species in the slice. This is stronger in its specialty with a tactical cost. One elite tier only; no infinite escalation or forced replacement of the normal form.

Progress is counted once per unique encounter target. Counts and unlocks survive failure. Save immediately after the qualifying bond, but apply the variant table only when the next run is created. Players can toggle elite research encounters off before departure; doing so does not remove the dossier or earned unlock.

## 7. Mage Power, food, and persistence

Interpret **Mage Power** as a bundle of Mage-specific XP/levels, skill points, and selected talents—not a separate spendable currency. Avoid a second permanent grind bar. Each level after 1 gives one point; prototype cap level 6 means five points available. Level costs are 100, 150, 200, 250, 300 XP (1,000 total). Ordinary encounters award 20 Mage XP, an optional elite 30, guardians 40, and final victory adds 40. A baseline full run with six ordinary fights and three guardians gives 280 XP; substituting one elite gives 290. Points are tied to the Mage who earned them.

**Small tree:** two branches, three ranks each including a shared root (five unique nodes). Each node costs one point, can be purchased once, and can be freely refunded in the Waystation. No respec mid-run.

| Node | Prerequisite | Effect |
|---|---|---|
| Field Training | None | Choose any affinity +1 at run start |
| Provision I | Field Training | Start with one Trail Crumb |
| Provision II | Provision I | Camp healing 35% → 40% |
| Bondcraft I | Field Training | First new recruit each run enters at full HP |
| Bondcraft II | Bondcraft I | Conduit grants an extra 4 Ward to its acting Sprite |

Talents add modest preparation/flexibility. Do not scale all enemy stats with Mage level; assess beginner and capped-Mage versions separately. Mage archetype differences should remain more important than the tree.

### Sprite growth within a run

Sprite level cap 5. Next-level XP costs: 30, 45, 60, 75 (210 cumulative). A level adds HP +6, Power +2, Guard +1, and no Speed. Increase current HP by 6 on level-up, preserving missing HP. Food gives XP to one selected Sprite; excess carries across levels and is lost at the level cap after an explicit warning. Regular fights grant each surviving active Sprite 6 XP and living reserve 3; guardians give 12 and 6. Downed Sprites gain none. New recruits start at level 1 with no inherited XP and 50% maximum HP after battle, unless Bondcraft I applies. The starter begins at full HP.

Food matching multiplies XP by 1.5 for the stated element, rounded down after all modifiers; universal food uses ×1. A normal Sprite at 0 XP eats a Grass Verdant Bite: 30 XP if Grass, 20 otherwise. At level 1, 30 XP reaches level 2 exactly. Kilnkeeper's Water-food penalty applies whether or not the recipient is Water; a matching Water meal with 20 base XP yields `floor(20 × 1.5 × .75) = 22`.

| Persists after any run | Resets after any run |
|---|---|
| Per-Mage XP/level/points/talents | Bonded individuals, their HP/XP/levels and reserve |
| Mage and starter species unlocks | Affinity allocations and route increases |
| Book pages, bonds/defeats, research and lore | Coins, food, consumables, equipped relics |
| Best depth, score, run summaries, settings | Bond charges, active effects, run route |

A first successful bond makes that common species a future starter option. Rare types and elites are not starters in the slice. The Book preserves the relationship's record; the fiction says expedition bonds are freely released at the Waystation. This reset is a major hypothesis: test whether it feels satisfying to a creature collector before investing in a larger roster.

## 8. Loot cascade: explicit probability contract

### Recommended interpretation

Treat the owner's 40/30/20/10 as **final unconditional shares among awarded random items**. One item is guaranteed per completed fight. Fixed coins, XP, and affinity rewards are separate and do not use this table. An optional no-item probability would require a separate explicitly named roll before this cascade; it is not enabled here.

For a desired rarity mass `p_i`, reached after all higher rarities failed, use `q_i = p_i / (1 − sum of higher p)`. Stop on the first success. Fresh conditional rolls are evaluated only if their stage is reached.

| Stage, tested in this order | Chance to reach | Conditional success | Final probability |
|---|---:|---:|---:|
| Legendary / Gold | 1 | 10% | 10% |
| Rare / Blue | .9 | 20 / 90 = 22.222…% | .9 × 2/9 = 20% |
| Uncommon / Green | .7 | 30 / 70 = 42.857…% | .7 × 3/7 = 30% |
| Common / Grey | .4 | 100% fallback | 40% |

They sum to 100%. Out of 10,000 random items, the mathematical expectations are 1,000 Legendary, 2,000 Rare, 3,000 Uncommon, 4,000 Common—not exact observed counts. In a nine-fight run the expected Legendary count is .9; the chance of at least one is `1 − .9^9 = 61.2579511%`. That is frequent for something named Legendary; retain the owner's example for testing, then decide whether to lower its final share. Do not quietly relabel a tuned percentage as a user requirement.

### If the numbers were intended as raw stage chances

Testing Legendary 10%, then Rare 20%, then Uncommon 30%, then falling back to Common yields final shares **10%, 18%, 21.6%, 50.4%**. If Common also rolls at 40%, its final share is **20.16%** and **30.24% is no drop**. Both interpretations are mathematically valid; neither matches 10/20/30/40 final shares. D05 must be resolved before implementation.

### Within-pool selection and edge cases

After choosing rarity, normalize that pool's positive eligible item weights. Item probability is `P(rarity) × weight / sum eligible weights`. With Rare items of weights 5, 3, 2, the first item's overall chance is `.20 × 5/10 = 10%`. Adding a Rare item of weight 5 changes that first item's overall chance to `.20 × 5/15 = 6.666…%`; Rare as a whole stays 20%, and all other rarities stay unchanged. **Pool independence does not mean individual items keep their odds.**

The sample item pools below use equal weight 1. Validate each pool has a positive total before an expedition. If all items are unavailable, use a defined fallback in the **same rarity**, never reroll the cascade. Common fallback: Trail Crumb; Uncommon: Growth Ration; Rare: Revival Ink; Legendary: Atlas Feast. These are always eligible and stackable. Invalid weights or probabilities fail content validation; they must not silently become another rarity.

Roll and persist one reward once. Opening/closing a panel, suspension, or replacing a relic does not reroll it. No pity or luck in this slice. If introduced later, describe how they change the rarity masses and expose the altered table. Bosses may grant fixed story rewards, but do not secretly alter the random item distribution.

## 9. Economy and the starter item set

One temporary currency: **field coins**, displayed as “Coins.” Start with 20. Ordinary fights award 12, elites 18, guardians 24; all living/defeated/bonded target combinations within the same cleared encounter yield the same fixed amount. A baseline full run earns `6 × 12 + 3 × 24 = 144`, or 164 including the starting purse. One elite replacing an ordinary adds 6. No permanent coin wallet and no end-of-run conversion.

Trader prices: tonic 18, bond charge 30, Growth Ration 24. One visit offers one of each, no refresh, no sales. Spending 18 + 30 + 24 = 72 leaves 92 of a full run's baseline budget if no other purchases occur; earlier shops may arrive before those earnings. Coins create an in-run choice between recovery, team access, and growth. Duplicates are consumable inventory, not a second salvage currency.

| Item | Rarity | Proposed effect | Pool weight |
|---|---|---|---:|
| Trail Crumb | Common | Universal food, 10 XP | 1 |
| Field Tonic | Common | Heal one living Sprite 18 HP | 1 |
| Cleanse Leaf | Common | Remove Scorch or Root from one ally | 1 |
| Verdant Bite | Uncommon | Food, 20 XP; Grass match ×1.5 | 1 |
| Growth Ration | Uncommon | Universal food, 20 XP | 1 |
| Bond Thread | Uncommon | Restore 1 bond charge, up to 3 | 1 |
| Astral Nectar | Rare | Food, 40 XP; Space match ×1.5 | 1 |
| Revival Ink | Rare | Revive one downed Sprite at 25% HP (floor, at least 1) | 1 |
| Copper Compass | Rare | Relic: once per encounter, first Guard grants 2 Focus instead of 1 | 1 |
| Atlas Feast | Legendary | Universal food, 70 XP | 1 |
| Lantern Heart | Legendary | Relic: first application of Scorch each encounter lasts 3 ticks | 1 |
| Last Page | Legendary | Relic: once per run, prevent the first active Sprite KO and set HP to 1 | 1 |

Two relic slots, no duplicate equipped relic. At full slots, compare and replace or discard; discarded relic grants nothing. Duplicate relic offers the same choice and does not reroll rarity. Consumables stack to 9 per item; a full stack triggers a keep/swap/discard choice with no silent destruction. Food is usable only outside combat; heal, cleanse, and revive items can be used in combat at the turn cost. Bond Thread is outside-combat only. Relic selection never costs a combat turn because it occurs between encounters.

**Pressure points:** .9 expected Legendary drops per run may overfeed growth; free 6/12 encounter XP may make food less valuable; retained XP on failure may encourage early resets. Measure these before adding currencies or escalating prices. Keep fastest XP acquisition tied to completing meaningful encounters; no rewards for entering, abandoning, or reloading a room. No energy timer, paid bond rolls, ads, or premium currency in the prototype. A commercial model requires its own owner decision and has not been selected here.

## 10. Art, audio, and narrative direction

**Working identity: The Living Atlas.** An expedition ledger in a world that is slowly losing its names. Sprites are living memories of environments: Cindermoth preserves warmth and old maps; Dewseal carries the shape of vanished streams. Mages use attunement to offer temporary bonds. Recording a creature restores a small part of the world's memory. A defeat means dispersal and observation rather than a requirement to depict death.

The Waystation is a modest traveling archive. The initial route, **The Reedglass Reach**, goes through a lantern grove, flooded paper ruins, and an observatory whose stars have disappeared. The chapter question is “Who benefits when a place is forgotten?” A guardian protects its region's memory rather than simply guarding loot. The first chapter reveals that the archive once removed dangerous memories deliberately; later chapters can ask whether every memory should be restored. This is a narrative direction, not a finished plot.

Use 1–2 sentence optional field notes after discoveries, short guardian exchanges before/after combat, and larger story beats at the Waystation. Never interrupt a routine turn with unskippable dialogue. First-run onboarding teaches movement, an effective hit, food, and bonding through four actions before introducing a tree.

**Approved visual direction:** the combat view and its in-scene Sprites are the owner's selected reference. Each combat must reflect the surrounding area. Sprites need body idle animations, idle emissive effects, and randomly cycling idle emotes. [ART_DIRECTION.md](ART_DIRECTION.md) records these requirements and proposes scene continuity, layered animation, timing, interruption, asset handoff, and acceptance checks.

**Remaining production proposals:** readable pixel characters on layered, atmospheric scenes; test native character resolutions before settling them; preserve silhouette, environmental grounding, and quiet command space. No resolution, engine, lighting technique, or animation frame budget has been approved. The other six original views, including the gouache character sheets and paper-dossier interface, are unapproved historical studies. Do not use them as production targets.

| Visual role | Proposal |
|---|---|
| Menus and Book | Visuals remain unresolved; the first paper-dossier presentation was not accepted |
| World mood | Moss and deep teal, ember amber, desaturated violet at distant ruins |
| Fire / Grass / Water | Ember flame / leaf-green sprig / cyan droplet, each with name and icon |
| Void / Space / Prismatic | Violet hollow circle / blue-white star / split-color diamond |
| Item rarities | Grey, green, blue, gold per U24; spelled-out labels and distinct borders |
| Type | Begin with the approved combat concept's legibility; typography for other screens requires a new design pass |
| VFX | Required idle emission and random emotes; proposed restrained intensity and clear priority for actions, HP, and intent |

Audio: field-recording-inspired wind, reed percussion, soft bell motifs for discovery; punchy short combat transients; each element has a distinct timbre. Music gains layers near a guardian. Separate sliders for music/effects, visual equivalents for important sounds, and haptics off by default during reduced-motion mode. No audio assets are delivered in this starter package.

**Future performance target:** steady 60 fps on agreed baseline devices, with a lower-effects 30 fps mode if necessary. Measure frame-time distribution and thermals, not only average FPS. Pixel art does not guarantee performance. Select representative low/mid-tier devices before choosing shaders, lighting, or engine.

## 11. Screen map and mockup contract

`Waystation → Mage / talents → Starter + affinity allocation → Route → Scene → Encounter → Reward → Route → Guardian → Run summary → Waystation`. The Book opens from preparation, scenes, rewards, and pause, and returns to the previous state. Bag and party management are available between encounters; combat shows only legal item actions.

See [wireframes/README.md](wireframes/README.md) and [the visual gallery](wireframes/index.html). The combat view is the sole accepted visual concept. The gallery places it first and labels all other views as unapproved historical studies. The mockups are not a functioning game, and their values do not imply approved or tested balance. SVG layouts remain editable and generated image prompts are preserved. No actual animation clips have been produced.

Screen review checklist: current actor obvious, enemy intent visible, affordability/eligibility inspectable, no unknown species pages, no offscreen confirm action, color-independent labels, a clear Back/Close control, and enough safe area for device cutouts. Insets and enlargement need interactive verification later.

## 12. Prototype tests and decision gates

No gameplay code is authorized by this document. Begin with printed cards, a die/random-number sheet, these screens, and a facilitator. Recruit 6–8 testers with a mix of party-RPG and mobile familiarity; this is a qualitative convenience sample, not statistically representative market evidence. Counterbalance scenario order and record prior experience. Ask for explanations and choices, not just a fun rating.

| Test | Method and sample task | Proposed acceptance signal | If it fails |
|---|---|---|---|
| T01: turn clarity | Each tester plays 3 paper fights; point to next actor, select skill, target, confirm | At least 6/8 can identify next actor and cost without help after the tutorial | Simplify queue/action layout before adding combat systems |
| T02: meaningful decisions | Compare elemental-only combat with a matched encounter using Resonance | At least 6/8 describe two plausible choices; typical fight ≤60 s after learning | Remove Resonance or shorten effects; do not add more meters |
| T03: bonding | Present eligible, low-affinity, high-HP, no-charge, and full-party cases | At least 7/8 explain each blocker and finish a legal bond without trial and error | Change wording/preview, not hidden probability |
| T04: collector expectations | Reveal expedition bond reset after one run; show persistent Book and starter unlock | At least 6/8 can explain what survives and say they want another expedition; inspect objections | Revisit D03; test a limited permanent companion model |
| T05: Book discovery | Discover through defeat, bond, and retreat; find one known habitat | No page for retreat-only sighting; at least 7/8 find a known requirement within 10 s | Rework indexing/entry hierarchy |
| T06: affinity agency | Offer safe-route heal versus +1 needed affinity and later rare habitat | At least 6/8 predict the consequence; choices vary between testers | Rebalance opportunity cost and preview reachability |
| T07: economy | Run 12 facilitated full expeditions across repeated sessions; track purchases and unused items | Both bonding and recovery purchased in at least 3 runs each; no mandatory single buy | Tune prices/sources; investigate skill differences |
| T08: research/elite | Simulate 3 repeated bonds, next-run elite, normal variant, and opt-out | All rules understood by 6/8; normal version still chosen in a credible scenario | Change variant cost before adding tiers |
| T09: mobile layout | Review landscape screens at actual phone size and enlarged text; compare portrait sketch | Confirm reachable; no essential clipped text; ≥90% first-tap target accuracy in later clickable test | Reflow; preserve target size before enlarging party |
| T10: interruption | Later approved prototype: suspend before/after action, reward, bond, level-up, and summary | Same state restored; no duplicate item, XP, or research | Fix persistence before expanding content |
| T11: loot contract | Exact algebra now; later use 100,000 draws with a known test seed | Final shares sum to 1; within-pool edit leaves other pools stable; observed rarity counts within 4 binomial standard deviations of expectation | Check semantics/eligibility; inspect seed and repeat diagnostic run |
| T12: frame pacing | Later prototype: 15-minute sessions on chosen baseline devices, normal and reduced effects | Target p95 frame time ≤16.7 ms in 60 fps mode; thermal behavior documented | Reduce effects/scene complexity before new assets |
| T13: area-specific combat | Compare each encounter scene with its surrounding area reference | Terrain, perspective, palette, and landmarks make the relationship clear | Recompose the battle within its area's visual language |
| T14: idle animation and emotes | Future 60–90 second group preview with commands interrupting idles | Seamless body loops, aligned restrained emission, varied asynchronous emotes, no delayed action or changed game state | Revise timing and priorities before expanding the roster |

The percentages above are provisional decision aids, not claims of validated usability. Log completion time, mistaken taps, action changes, unused charges, food wasted at cap, damage by element, retreat depth, bond attempts/eligibility, Book openings, and replay intent. For paper tests, collect manually without accounts or telemetry services. If later instrumenting, collect only the data needed for these questions and decide storage/consent before implementation.

### Probability and economy acceptance cases

- Exact stage products: .1; .9 × 2/9 = .2; .7 × 3/7 = .3; .4 × 1 = .4.
- A threshold roll exactly equal to a conditional probability fails when using intervals `[0,q)`; values must be sampled in `[0,1)`. Common always succeeds. This removes boundary ambiguity.
- Empty/all-zero pool invokes the same-rarity fallback; negative/invalid weights are rejected before run creation.
- Adding a Rare item changes only Rare conditional item weights, not the four rarity masses.
- Bonded targets generate one encounter reward, even if released; full team/stack choices cannot duplicate it.
- Level 5 food prompts about waste; no XP-to-coins or hidden permanent conversion.
- Suspended reward resumes the same selected item; defeat, retreat, and force-close do not reroll.

### Gates

**Gate A—preproduction review:** combat art direction is selected; owner still resolves D01–D07 and reviews the six-type matrix, reset rule, replacement noncombat views, and animation samples. **Gate B—paper validation:** T01–T08 show the loop works; documented failures become revisions. **Gate C—separate implementation authorization:** select engine and baseline devices, plan data/save boundaries, and read the copied engineering policy before coding. **Gate D—small playable slice:** test T09–T14 and stop content expansion until the save, economy, animation, and pacing risks are understood.

The most consequential unresolved question is whether temporary Sprite bonds plus a permanent dossier satisfy the desired collector fantasy. Resolve that before commissioning a large bestiary.
