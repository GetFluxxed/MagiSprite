# MagiSprite — source requirements

Version 0.2 · Preproduction only · Updated after the owner's visual review

This document records what the owner actually specified. It is a product requirements record, not a chosen software architecture. Sources are [ORIGINAL_BRIEF.md](reference/ORIGINAL_BRIEF.md) and the later [visual feedback](reference/VISUAL_FEEDBACK.md). The package request adds economy, cascade mathematics, a test plan, and packaging. The later review selects the combat concept and adds animation and repository requirements. Proposed answers live in [DESIGN.md](DESIGN.md); they are not approved requirements unless explicitly recorded here.

**Status key:** **Stated** = an explicit requirement or preference; **Tentative** = the owner used language such as “perhaps,” “might,” or “maybe”; **Open** = the source does not decide it. Tentative statements must not silently become fixed rules.

## 1. Product and scope

| ID | Status | Source requirement |
|---|---|---|
| U01 | Stated | A mobile game with a compelling, repeatable creature-collecting roguelite loop. The owner describes the ambition as “if Pokemon was Final Fantasy.” |
| U02 | Stated | Rather fast-paced, streamlined gameplay, smooth frames, interesting combat, and deliberate narrative and art direction. “Fast-paced” does not override the explicit turn-based preference. |
| U03 | Stated | Flesh out mechanics, items, creatures, characters, and game loop before writing gameplay code. This delivery is preproduction only. |
| U04 | Stated, working terminology | Creatures are **Sprites**; the player character is a **Sprite Mage**. The owner allows the names to change later. |
| U05 | Open | World name and its relationship to the creatures. Naming the world after them was considered, not selected. |

## 2. Run-to-run progression and collection

| ID | Status | Source requirement |
|---|---|---|
| U06 | Stated | **Mage Power** and the **Sprite Book** carry over between runs. What Mage Power contains is not defined. |
| U07 | Stated | The Sprite Book should resemble a dossier or entry book. |
| U08 | Stated | Undiscovered Sprite pages are absent from the book. A page is made after discovering a Sprite through capturing or defeating it. No blank silhouette-filled catalogue was requested. |
| U09 | Tentative | Collecting a Sprite an unspecified **x** times may unlock stronger or elite variants of that Sprite in future encounters. |
| U10 | Stated intent for U09 | Use continued discovery of stronger creatures to support engagement, higher scores/progress, and build diversity. Elite unlock count, strength curve, and limits remain open. |
| U11 | Stated | Playing a specific Mage grants experience and Mage-specific levels. |
| U12 | Stated | These levels unlock points in a greater skill tree. Start with small, manageable trees for testing and expand after testing. |

The brief does **not** establish persistent ownership of individual captured Sprites, run loss rules, a persistent kennel, Sprite permadeath, a permanent item inventory, or account-wide skill points. Persistent knowledge and persistent creatures are different decisions.

## 3. Sprite Mages and bonding

| ID | Status | Source requirement |
|---|---|---|
| U13 | Stated | Mages form bonds with Sprites as the collection mechanism. Whether bonding is possible depends on the player's **current stats**. |
| U14 | Stated | Unlockable base Mage archetypes, inspired by Risk of Rain 2's unlockable character archetypes. No specific unlock method was selected. |
| U15 | Stated | Mages have different affinities, boosts, or build synergies. |
| U16 | Stated | The basic Mage should be able to do everything and be fun broadly. Specialist/alternative Mages should have specific drawbacks and downsides. |

Open: which stats determine bonding, thresholds, whether eligibility guarantees success, capture cost/timing, number of bond attempts, party/reserve size, whether the Mage is a combat actor, and whether specialists can ever access all elements. No random capture chance was specified.

## 4. Elements

| ID | Status | Source requirement |
|---|---|---|
| U17 | Stated | An elemental system determines Sprite strengths and weaknesses. |
| U18 | Tentative | Approximately six colors/types. Fire, Grass, and Water are the three most abundant. The brief explicitly writes **Fire > Grass > Water**. |
| U19 | Tentative | Two rarer, rarely obtainable types, potentially **Void** and **Space**, are effective against each other. |
| U20 | Tentative | A sixth type, **Prismatic**, has no default strength or weakness and might learn moves from all six types. |

The closing edge Water > Fire is **not written in the brief**. A complete three-element cycle is a reasonable proposal, not a source fact. Same-element resistance, damage multipliers, dual types, type colors, move typing versus creature typing, and how Prismatic learned attacks interact with neutrality are all open. The user did not tie creature rarity to drop rarity.

## 5. Sprite Food, drops, and rarity

| ID | Status | Source requirement |
|---|---|---|
| U21 | Stated | Sprite Food can upgrade Sprites during a run, taking slight inspiration from Summoners War's summon upgrading. |
| U22 | Stated | Different foods have different drop rates and grant corresponding amounts of Sprite experience. |
| U23 | Tentative | Food rarity or type may make it better for particular elemental Sprites. |
| U24 | Stated, initial scope | Four initial item/drop rarities: **Common—Grey; Uncommon—Green; Rare—Blue; Legendary—Gold**. |
| U25 | Stated | A robust drop system with a separate table for each rarity. Select rarity first, then an item within the selected rarity's pool. |
| U26 | Stated | Test Legendary first; on failure cascade to Rare and onward. A successful rarity roll is followed by a selection among eligible items in that pool. |
| U27 | Stated intent | Editing items within one rarity pool should not change the probabilities of other rarity pools. |
| U28 | Tentative example | Example numbers: 40% “normal,” 30% Uncommon, 20% Rare, 10% Legendary. “Normal” appears to refer to Common, but that terminology is not formally resolved. |

**Mathematical ambiguity:** Those four numbers can be desired final probabilities or per-stage conditional success rates. They produce different results in a sequential cascade. The brief does not resolve which meaning is intended. Common as guaranteed fallback versus a fallible roll, a no-drop outcome, number of drops per encounter, within-pool weights, duplicate handling, luck/pity, and empty pools are also open. See DESIGN §8 for an explicit proposed interpretation and both calculations.

## 6. Combat and art

| ID | Status | Source requirement |
|---|---|---|
| U29 | Stated | Turn-based, team-focused combat with a Final Fantasy-style layout. |
| U30 | Stated | Select and target actions; each Sprite has an individual turn, its own actions and skillset. Consumables are part of combat. |
| U31 | Stated | Some form of **pixel art**. |
| U32 | Stated references, not a fixed technique | Inspiration from Octopath Traveler 1 and 2 and older Final Fantasy titles, including 1 and 2. The original brief left the precise pixel style undecided; the later combat concept approval is recorded in U38. No engine, 3D pipeline, lighting method, asset resolution, or camera specification was selected. |

### Later owner review: accepted combat direction

| ID | Status | Owner requirement |
|---|---|---|
| U38 | Approved visual direction | Only the combat view is liked as the concept for how the game should look. The Sprites shown in that scene are endorsed. The other views are not approved visual directions. |
| U39 | Stated | Render each combat in the scene of the surrounding area. A shared scene instance versus an area-matched battle composition remains undecided. |
| U40 | Stated | Sprites need idle body animations during combat. |
| U41 | Stated | Sprites need idle emissive effects during combat. |
| U42 | Stated | Sprites need emotes that can cycle randomly during combat. |
| U43 | Stated | Make this project a GitHub repository connected to `https://github.com/GetFluxxed/MagiSprite.git`. |

The approved reference is [03-combat.png](wireframes/03-combat.png), with [its source scene](wireframes/assets/reedglass-combat.png). [ART_DIRECTION.md](ART_DIRECTION.md) separates accepted requirements from proposed animation details. Visual approval does not approve every example number, UI control, party size, or mechanic in the mockup. The Sprite Book and progression systems remain required although their first visual mockups were not accepted.

Open: turn order, team size, attack formulas, resource model, statuses, critical hits, retreat, revive rules, animation timing, portrait/landscape orientation, overworld control scheme, and accessibility options. “Idle in the game world” requests a visual state; it does not establish idle-game automation or offline rewards.

## 7. Deliverables and provenance

| ID | Status | Current delivery requirement |
|---|---|---|
| U33 | Stated | ARCHITECTURE.md accurately records source mechanics and unresolved choices. |
| U34 | Stated | DESIGN.md interprets and thoughtfully expands the design, clearly separating proposals from source decisions. Include combat, runs, progression, Book, affinity/bonding, cascade math, economy, art, narrative, and prototype tests. |
| U35 | Stated | A wireframes/ folder with visually compelling Sprite, Mage, combat, exploration/idle, Book, and progression sketches/mockups. |
| U36 | Stated | Find and copy the existing ENGINEERING.md from the “Portfolio Website Planning” context. Do not fabricate a replacement. |
| U37 | Stated | Bundle starter files for download; a ZIP is welcome. Do not write gameplay code. |

The located “Portfolio Website Planning” conversation is in the project listed by the app as “Photography Portfolio Template.” An existing downloaded ENGINEERING.md was copied byte-for-byte; source details and the limits of the remote comparison are in [PROVENANCE.md](reference/PROVENANCE.md). Its own version remains Draft 0.1. Copying it does not promote it to an approved 1.0 policy.

## 8. Decisions to make before a playable prototype

| Decision | Why it matters | Proposed answer to evaluate |
|---|---|---|
| D01: party, Mage role, orientation | Sets pacing, touch targets, content workload | Three active Sprites, one reserve; Mage as support command; landscape |
| D02: bonding and six affinities | Determines whether builds are expressive or frustrating | Transparent deterministic eligibility; temporary run affinities |
| D03: what survives a run | Defines collector expectations | Mage XP, Book, unlocks; individual bonds reset |
| D04: elemental completion/Prismatic | Prevents hidden exceptions | Complete cycle; Prismatic attacks stay neutral |
| D05: cascade semantics | Prevents incorrect loot distribution | Treat 40/30/20/10 as final shares; Common fallback |
| D06: elite research | Avoids unbounded power creep or collection grind | Three bonds unlock an optional sidegrade encounter variant |
| D07: session length and failure | Sets mobile structure | 12–18 minute run; save at every decision; retained discoveries |
| D08: business model and network | Changes economy and future engineering scope | Offline prototype with no monetization; commercial model deferred |
| D09: art technique and baseline devices | Controls production cost and performance | Combat scene direction accepted under U38–U39; implementation, pixel resolution, and baseline devices still open |
| D10: animation production | Controls asset scope and readability | Body idle + emission + random emotes required; clip counts, timings, scheduling, tools, and emission technique proposed in ART_DIRECTION.md |
| D11: other screen designs | The first noncombat views were not accepted | Redesign them using the approved combat reference; no replacement design approved yet |

The final column separates the approved direction in U38–U42 from remaining **proposals**. No engine, backend, account system, analytics service, payment provider, or production technology has been chosen.
