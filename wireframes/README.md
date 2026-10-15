# MagiSprite — visual reference status

Open [index.html](index.html) for the local gallery. **Only 03-combat is the owner's accepted visual concept.** Its in-scene Sprites are endorsed. All other views are unapproved historical studies and must not be used as production design targets. Read [the owner's feedback](../reference/VISUAL_FEEDBACK.md) and [ART_DIRECTION.md](../ART_DIRECTION.md) for scene continuity and required idle animations, emission, and randomized emotes.

PNG files are previews; matching SVG files contain editable screen labels and shapes with embedded scene art. No animation sheets or clips have been produced. Original art is kept unchanged, so older presentation captions may still say “proposed”; the approval status in this guide and gallery takes precedence.

| No. | Artifact | Owner review status |
|---|---|---|
| 03 | [Combat PNG](03-combat.png) · [SVG](03-combat.svg) | **Accepted concept direction**, including the in-scene Sprites; example rules/numbers remain proposals |
| 01 | [Cindermoth sheet](01-sprite-cindermoth.png) | Unapproved historical character-sheet treatment; use the combat Sprite reference instead |
| 02 | [The Wayfarer sheet](02-sprite-mage-wayfarer.png) | Unapproved historical study |
| 04 | [Exploration PNG](04-exploration.png) · [SVG](04-exploration.svg) | Unapproved visual direction; redesign pending |
| 05 | [Sprite Book PNG](05-sprite-book.png) · [SVG](05-sprite-book.svg) | Unapproved visual direction; Book mechanics remain in scope |
| 06 | [Progression PNG](06-progression.png) · [SVG](06-progression.svg) | Unapproved visual direction; Mage progression remains in scope |
| 07 | [Bonding PNG](07-bonding.png) · [SVG](07-bonding.svg) | Unapproved visual direction; bonding mechanics remain in scope |

The screen boards use a **960 × 540 logical landscape layout**, rendered inside a 1600 × 1180 presentation board. Decorative board captions are not game UI. Screens show distinct review states; they are not a sequential playthrough. No buttons execute gameplay.

## Scenario values and deliberate limits

- Combat and bonding use a scripted encounter sheet: Cindermoth Power 20, Focus 3, Speed 8; both Bramblebacks maximum HP 60, Guard 8, Speed 6. This deliberately overrides the general role-stat suggestions for these enemy test sheets. Target A has 36 HP; target B has 18 HP. Grass affinity 2 and two bond charges make B eligible. The other allies have Speed 8; stable party order breaks ties. Cindermoth's Fire attack deals `(20 × 1.4 − 8 × .5) × 1.5 = 36` damage. The combat board is before confirming that attack. The bonding board is an alternate choice at the same decision, not the result of the attack.
- The exploration scene is an independent choice-node example. Its coin purse reflects prior play, not an asserted node-by-node economy simulation. The Mage is idle waiting for input; there is no income timer. In the proposed interaction, either a marker or its much larger label can be tapped.
- The Book has seven discovered pages, including a previously bonded Cindermoth with two research bonds. Folio numbers reflect discovery order. The threshold of three is a proposal; the full population and undiscovered species are absent.
- The progression screen has a level-3 Wayfarer, two total earned points, one owned node, and one unspent point. Its 80/200 XP bar is progress toward level 4. Provision I is selected for inspection but not purchased.
- The unapproved concept sheets use gouache, graphite, and small pixel studies. Their designs differ from the separately generated in-scene characters. Future production sheets must follow the **endorsed combat appearance**; do not force it to match the earlier unapproved sheets. No engine, rendering pipeline, or animation budget is established.
- These are legible desktop boards and touch-layout hypotheses. Device safe areas, text enlargement, real touch accuracy, screen-reader behavior, and frame pacing still require interactive testing. Body copy at phone scale may require reflow; do not treat these drawings as accessibility certification.

## Editing and review

1. Change approved design rules in DESIGN.md first; keep source requirements separate in ARCHITECTURE.md.
2. Edit screen SVG copy/layout in a vector editor. Embedded raster artwork remains the concept reference.
3. Export a PNG at 1600 × 1180 after a layout change and compare it visually with the SVG.
4. Keep the filename stable when revising a screen; save materially different directions as new numbered studies.
5. Update these scenario notes if values change. The static gallery uses the PNG previews.

Generated source scenes are in [assets/](assets/), and the full generation prompts are in [IMAGE_PROMPTS.md](IMAGE_PROMPTS.md). No external images, remote fonts, or live services are required to view the gallery.
