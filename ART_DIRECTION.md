# MagiSprite — combat visual direction

Status: **owner-selected combat concept; animation specification proposed**.

![Approved combat concept](wireframes/03-combat.png)

The owner selected this combat view as the sole visual reference for how the game should look in concept. The Sprites within this scene are endorsed. Read [the exact feedback](reference/VISUAL_FEEDBACK.md) and requirements U38–U43 in [ARCHITECTURE.md](ARCHITECTURE.md). Approval of this image is not a balance or implementation approval.

## 1. What is established

1. Use the combat view's in-scene presentation as the visual target.
2. Render each combat in the surrounding area's setting.
3. Animate Sprite idle poses in combat.
4. Include idle emissive effects.
5. Give Sprites emotes that can cycle randomly during combat.

The other views are unapproved historical studies. In particular, the illustrated paper dossier layout, Mage portrait sheet, overworld screen, progression screen, and bonding panel do not define the future game's interface. The underlying Sprite Book and Mage progression requirements remain; their visuals need a new pass informed by the combat concept.

## 2. Reading the approved reference — proposed production rules

These are interpretations to test, not extra owner decisions:

- Sprites inhabit the scene with grounded placement, contact shadows, consistent perspective, and readable separation from the background.
- Keep the battle area's environmental identity: terrain, architecture, vegetation, palette, and ambient lighting. A marsh encounter should retain marsh ground, water, reeds, and local ruins; a cave encounter should retain its rock, enclosed lighting, and material cues.
- Compose readable opposing formations within that local environment. Preserve a quiet command area and enough space for targets and effects without obscuring the creatures.
- Retain the compact pixel-like creature silhouettes, rich environmental depth, and restrained dark combat panels as the starting direction. Native pixel resolution, shading method, exact fonts, and shader effects are still open.
- Let ambient motion continue during player decisions. This makes a paused tactical decision feel alive without introducing a real-time input requirement.

**Scene continuity requirement:** the encounter must visibly belong to the place it occurs. Reusing the exact exploration scene/camera versus loading a matching battle composition is an open technical choice. The user's request does not settle camera transitions, free-roam movement, 2D versus 2.5D, or engine selection.

**Encounter-art proposal:** each area supplies a terrain/lighting reference, foreground and background treatment, safe party/enemy anchor regions, and rules for occluding foliage. Time-of-day or weather matching is desirable if those systems are later adopted; neither system is required by this approval alone. Do not substitute the same unrelated arena for every biome.

## 3. Three animation layers

| Layer | Role | Proposed starting treatment |
|---|---|---|
| Body idle | Sustained life and weight | Seamless breathing, wing movement, tail/ear shifts, or stance motion; each Sprite starts at a different loop phase |
| Idle emission | Elemental material and atmosphere | Separate glow/emission treatment for authored regions, plus optional small particles; stays aligned with body frames |
| Idle emote | Occasional personality | Short antenna twitch, glance, stretch, sniff, chirp pose, paw adjustment, or shell shake; return to the ordinary idle pose |

An emissive region is not the same as a large screen-space bloom. Keep highlights localized and readable, including on bright terrain. Ordinary body colors and shadows still need to work when effects are reduced. Whether emission affects nearby terrain, uses an additive sprite layer, or uses a lighting shader remains undecided.

Suggested species studies drawn from the **combat scene**, not the unapproved character sheets:

| Sprite | Body idle proposal | Emissive proposal | Two emote proposals |
|---|---|---|---|
| Cindermoth | Uneven wingbeat with a small hovering bob; legs settle independently | Lantern abdomen slowly brightens and dims; occasional faint ember | Antennae search the air; brief wing flare then settle |
| Dewseal | Chest breath, soft body squash, flipper adjustment | Restrained cool highlights on dew/lily edges; one tiny glint | Curious head tilt; small flipper wave |
| Fernwhisk | Ear tips sway, breath, tail flick | Subtle leaf-vein shimmer with very low intensity | Sniff the air; paw groom |
| Brambleback | Heavy breath and minute shell lift; planted feet | Sparse glowing seed points or pollen near shell flowers | Short shell shake; look over shoulder |

Emission motifs beyond Cindermoth's obvious lantern are proposals requiring review. Do not reinterpret the visual approval as a requirement to make every surface glow.

## 4. Random emote behavior — proposed contract

- Eligible only while an alive Sprite is in an ordinary idle state. Targeting, actions, hit reactions, bonding, defeat, and important combat signals take priority.
- Start with a weighted selection among 2 emotes per species, excluding the immediately previous emote. Timing and identity both vary, rather than cycling all actors in sync.
- Proposed first test: each actor waits a random **15–30 seconds** of eligible idle time. A shared **6–10 second** gap between emotes and a maximum of **one idle emote at a time** keep a five-actor battle quiet. Randomize the first delay too.
- When selected for a command, return the actor to a stable readable pose; allow low-amplitude body idle and localized emission. Emotes never move its target anchor or change hitbox, stats, turn order, Focus, rewards, or bond eligibility.
- An action can interrupt an emote immediately at a safe pose transition. The action must not wait for an idle animation to finish. Finish or smoothly blend an interrupted glow without a sudden full-screen flash.
- Pause timers when backgrounded or paused. Resume with a fresh idle delay; do not replay a backlog of emotes. Cosmetic randomness must not advance any gameplay/loot random sequence.
- With reduced motion, provide a still or minimal-motion idle, constant low-intensity emission, and disabled flourish emotes/particles. Intents, statuses, selection rings, and elemental labels remain visible independently of these effects.

All intervals are test proposals. The accepted requirement is varied idle emotes during combat, not these particular seconds or weights.

## 5. Asset handoff proposal

Begin with Cindermoth, then validate the process on Dewseal before expanding the roster. These are future production tasks; no animation sheets or playable animation system are delivered yet.

- Create one consistent model and palette from the combat reference at an agreed native pixel size. The flattened concept image cannot supply occluded frames or clean animation layers automatically.
- Author a seamless body idle loop. Initial trial: 6–8 frames at 8–12 frames per second, with deliberate frame holds where the creature's weight benefits. Display/frame-render rate is independent of sprite-animation frame rate.
- Supply 2 short emote clips per species, provisionally 0.6–1.2 seconds each, with documented return/interruption poses. Approve timing by viewing motion, not by meeting a frame count.
- Provide aligned transparent body frames, an optional per-frame emission mask/layer, consistent canvas dimensions and pivot, and a separate contact-shadow treatment where needed. Frame names and timing metadata should be portable and documented; no engine-specific format is selected here.
- Keep neutral, selected, action-ready, and defeated visual states distinguishable. Required attack/hit/defeat animation coverage is a later production scope decision, not satisfied by an idle loop.
- Preview the animation against both dark and light representative area backgrounds, with effects on and off, at actual mobile display size.

## 6. Review gates

| Check | Pass condition |
|---|---|
| Area identity | A reviewer can tell the battle belongs to its surrounding location from terrain, palette, and set dressing |
| Character fidelity | Body proportions, silhouette, and personality agree with the endorsed in-combat Sprites |
| Loop seam | At least ten repeated loops show no visible pop, sliding pivot, or mismatched glow |
| Idle variety | A 60–90 second group preview shows asynchronous movement and occasional varied emotes without coordinated repetition |
| Turn responsiveness | Commands interrupt emotes promptly and never wait for a flourish; no game-state change comes from cosmetics |
| Effect readability | HP, enemy intent, element labels, and selected targets remain readable with every glow active |
| Reduced effects | The scene still communicates state with emotes/particles disabled and emission flattened |
| Asset portability | A human can locate source frames, emission layers, pivots, and timing without reconstructing the original conversation |

Actual animation, frame pacing, and device performance remain untested. Do not present this specification or the static concept as an animation prototype.
