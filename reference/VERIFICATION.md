# Verification record

## Repository revision 0.2

The later owner review selects the combat concept, requires battles in their surrounding area, and adds idle body animation, idle emission, and randomized emotes. ARCHITECTURE.md records these as U38–U43; ART_DIRECTION.md distinguishes requirements from proposed production details. Other views are explicitly labeled unapproved historical studies in the README, design, wireframe guide, and gallery.

This revision creates the MagiSprite repository from the preproduction package. No animation clips, new rendered artwork, engine, gameplay implementation, or deployed website are included. The original 0.1 download remains a historical snapshot, while this repository contains the current review status. Local machine paths and private conversation identifiers were removed from the repository's source headers/provenance; the engineering policy and artwork bytes remain unchanged.

The original checks below describe the initial package. Repository checks confirmed 43 unique requirement IDs, 44 local Markdown references, a combat-first gallery with six collapsed unapproved studies, and byte preservation of ENGINEERING.md, all nine PNGs, and all five SVGs. The refreshed manifest covers 28 files before the manifest itself, and no credential/archive files are selected. Git publication is checked separately by comparing remote main with the local commit after push; this document is not itself evidence of a remote write.

The whitespace check preserves an intentional source-format exception: ENGINEERING.md has two Markdown hard line breaks expressed as trailing spaces on its Version/Status lines. Its bytes must remain unchanged, so that copied file is excluded from the whitespace-only diff check. All newly authored or edited text is checked normally.

## Original package review

2026-10-14 · Preproduction review, not validation of a playable game.

## Performed

| Check | Observed result |
|---|---|
| Full source recovery | The game conversation returned its complete user message with no further page; original preserved in reference/ORIGINAL_BRIEF.md |
| Requirement review | ARCHITECTURE.md separates 37 source/delivery requirements into stated, tentative, and open, including the incomplete elemental cycle and ambiguous drop percentages |
| Scope review | Package contains documents, generated reference art, static SVG layouts, PNG previews, and an HTML/CSS gallery; no gameplay, engine project, runtime services, or dependency manifest |
| Engineering-file identity | Source and package copy are both 20,136 bytes; byte comparison and SHA-256 match `e1a2cffa11f781d6a1d63bbaebc1e2890ddea2b83ba47ae6807951d2604ad1a5` |
| Proposed cascade algebra | Exact rational calculation gives 1/10, 1/5, 3/10, 2/5; total 1 |
| Literal cascade alternative | Calculated 10%, 18%, 21.6%, 50.4% with Common fallback; 20.16% Common and 30.24% no drop if Common rolls at 40% |
| Nine-fight Legendary chance | Exact calculation of 1 − .9^9 = .612579511 |
| Economy and progression arithmetic | Checked 280 baseline full-run Mage XP; 164 coins including starting purse; 1,000 XP across five Mage levels; 210 XP across four Sprite levels |
| Combat/bond example | Checked 36 damage using Power 20, potency 1.4, Guard 8 and ×1.5; 18/60 HP equals 30%; corrected the mockup queue to match the scripted Speed values |
| SVG validity | All five SVG screen files parsed as XML and rendered successfully to 1600 × 1180 PNGs |
| Image integrity | All nine PNGs opened and passed image decode verification: two concept sheets, five rendered screens, two source scenes |
| Visual review | Inspected both generated character sheets and both scene references; inspected all five screen PNGs; moved combat overlays to reveal creatures and avoid overlaps; inspected updated combat PNG |
| Local references | Checked Markdown and gallery paths; all point to bundled local files (manifest/report generated during final packaging) |
| Gallery scope | HTML parsed; no script element, remote asset, remote font, or external URL dependency |

## Fidelity map

| Source requirements | Where the proposal responds |
|---|---|
| U01–U05: identity, mobile pace, preproduction | DESIGN §§0–2, §10; character concept sheets |
| U06–U12: persistence, dossier, elite possibility, Mage levels/tree | DESIGN §§6–7; Book and progression screens |
| U13–U16: current-stat bonds and Mage archetypes | DESIGN §4; bonding screen |
| U17–U20: tentative six-element system | DESIGN §5; explicit full matrix and Prismatic interpretation |
| U21–U28: food, four colors, separate rarity pools and cascade | DESIGN §§7–9; both probability interpretations |
| U29–U32: individual turns and pixel-art direction | DESIGN §§3, 10–11; combat/exploration mockups |
| U33–U37: requested package | README.md, this record, provenance, copied policy, and ZIP delivery |

## Not performed / limits

- No user playtest has taken place. Run duration, fun, replay intent, tree balance, economy balance, and collector satisfaction remain hypotheses.
- No gameplay implementation, save-system test, Monte Carlo runtime test, frame-time measurement, phone touch test, screen-reader audit, or device accessibility certification was performed. DESIGN §12 defines proposed future tests.
- The static gallery's paths and structure were checked; it was not exhaustively tested across browsers. PNGs were directly rendered and visually inspected.
- Generated art is a concept reference. Exact model consistency, palette discipline, production pixel grids, animation frames, rigging, and export pivots have not been established.
- The ENGINEERING.md copy is verified against the user's existing local download. The portfolio conversation corroborates its origin, but original remote attachment bytes were not available for comparison. See PROVENANCE.md.
- These checks demonstrate package integrity and internally checked examples, not that the proposed game is balanced or technically ready to ship.

The final ZIP is created from the completed package, tested for archive integrity, and checked against the file manifest during packaging. The manifest excludes only itself.
