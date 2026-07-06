# Visual Improvement Log — Monaco GP Circuit Walk

Baseline (build session): `screenshots/02-harbor-golden.png`, `03-tunnel.png`, `04-night-pits.png`, `06-casino.png`

## Pass 1 — 2026-07-05
Verified side-by-side at identical camera positions/hours. Night fps 60, day fps 68, zero console errors.

**Kept:**
- Per-building window tiling (`facadeM(base, rx, ry)`): casino, hotel, city infill, hillside apartments now show correctly-scaled window grids instead of 13m-wide stretched slabs. Biggest single win (see p1-casino vs 06-casino).
- Night-only bloom (EffectComposer + UnrealBloomPass, threshold 1.0, strength .45, gated on `lightsF > 0.65`): floodlight halos, glowing lamp globes, blooming start-gantry lights (p1-night vs 04-night-pits). Day render path untouched.
- Warm Mediterranean paving texture (512px, per-tile tint variation + joints) replacing the flat gray-lavender ground.
- Hillside rebuilt: near ridges lowered/warmed, second lighter far ridge added, apartments 240 → 380 with tiled windows — skyline now dense city instead of khaki wall (p1-harbor vs 02-harbor).
- Life/motion: 4 gulls circling the harbor with flapping wings (one crosses the sun disc in p1-harbor), palm crown sway, flag flutter around poles, fountain jet pulse, background yachts bob/roll.
- Fixes: bg-yacht glass band softened + masts added, NPC heads .14 → .115 with softer skin tones.

**Tried and reverted:**
- Always-on bloom (threshold .85 → whole-frame milky wash; custom sky/water shaders lose saturation under OutputPass tone mapping — root cause of two bad iterations).
- Compensating shader-output multipliers (×1.3) — brightened the milk instead of restoring saturation.

## Pass 2 — 2026-07-05
Verified at the same casino/tunnel/harbor angles. 62 fps, zero console errors.

**Kept:**
- Plaza + pool-deck paving texture (warm stone tiles, per-tile tint, soft grout) — the plaza no longer reads as a flat mauve slab (p2-casino vs p1-casino).
- Casino facade pilasters + roof balustrade with posts — Belle Époque relief instead of a flat box.
- Tunnel interior: pale wall bands + white floor-edge guide-light strips on both segments — much stronger depth read (p2-tunnel vs 03-tunnel).
- Quay drop walls: stone-course texture with algae waterline band (visible from the gangplank, p2-gangplank); waterline foam strips around the basin.
- Street furniture: 14 wooden benches (promenades, plaza, pool) + ~60 cast-iron bollards along the quay; grandstand canopy lightened with cream underside.

**Tried and reverted:**
- Dress silhouette with fitted bodice (two variants: cone+waist+shoulder box, then cone+flared bodice) — both read as chess pawns up close; reverted to the clean cone which photographs elegantly.

## Pass 3 — 2026-07-05
62 fps day and night, zero console errors. No collision changes.

**Kept:**
- Moon: disc + halo in the sky shader (night-gated) **and** a moonlight glitter path on the water — the p3-night-harbor shot is now the best frame in the demo.
- Night water fix: base water color dims to 18% at full night — was glowing neon cyan (visible in the first p3 night shot); now dark navy with moon sparkle + warm quay-light spill.
- Lamp light pools: additive ground discs under all 22 street lamps, opacity driven by the day-night cycle.
- Supercar running lights: emissive tail (red) and headlight (warm white) strips on all 7 parked cars, night-gated.
- Yacht deck furniture: sunpads, teak table, champagne bucket, stools — the walkable deck is no longer bare.
- Portal header slab + repositioned TUNNEL sign (was clipped by the arch); cloth ripple on the 5 promenade flags (segmented plane, per-vertex wave) replacing the rigid rotating boards.

## Pass 4 — 2026-07-05
62 fps, zero console errors. Spawn→pits walking leg re-verified after adding grid-car colliders (0 fails).

**Kept:**
- Race dressing on the S/F straight: fictional sponsor banner strip (Riviera Bank / Azur Jets / Chrono d'Or / Monarque) on both faces of the pit wall + grandstand front, a sponsor bridge over the track at z −80, two F1 cars parked on the starting grid, marshal huts, and a 10-tyre barrier line at Ste Dévote (p4-straight, p4-grandstand).
- Grandstand crowd now sits in fan sections (red / orange / blue / mixed blocks) instead of uniform confetti.
- Casino lobby: wine-red wall panels, gold skirting + cornice trim, gilded door frame, second chandelier (p4-lobby).
- Golden-hour haze: fog near/far tighten around 18:00 for warm depth, relaxing again by night.

**Fixed during the pass:** first version of the lobby "gold trim" rendered as 5.6 m orange slabs — reduced to proper skirting/cornice strips before keeping.

## Pass 5 — 2026-07-05
65 fps, zero console errors. No collision changes (parade cars are non-colliding "ghosts" by design).

**Kept:**
- Two demo F1 cars (blue + red, half a lap apart) doing continuous parade laps of the full circuit along the track spline — through Casino Square at plaza height, down the tunnel slope, around the pool chicane. Verified numerically: 19 m/s along the curve with correct elevation (y 6.1 on the plaza). Slowed from an untrackable 26 m/s so players can actually watch them.
- Helicopter circling the harbor at ~60 m with spinning main/tail rotors and banked attitude — clearly visible from the promenades (p5-harbor-life).
- Six red/white buoys bobbing and rocking in the harbor; mooring lines (sagging tube curves) from the AURELIA's stern to the quay.
- Boutique doorway light pools added to the night light-pool mesh.

**Process note:** spent several attempts trying to photograph the moving car — screenshot round-trip latency (~1s ≈ 20 m of travel) makes stills a coin flip; motion is verified via position sampling instead (39 m covered in 1.5 s pre-slowdown).

## Pass 6 — 2026-07-05
62 fps, zero console errors. Spawn→pits walk leg re-verified after grid-car realignment (0 fails).

**Kept:**
- Positional parade-car engine voice: continuous dual-saw oscillator whose gain follows the nearest demo car (inverse-square to 120 m) with doppler pitch from radial velocity. (Code-verified only — headless can't audition audio; patterns match the proven ambient engine synth.)
- Plaza planters: 15 topiary hedges in terracotta pots along the south balustrade + corners (p6-planters — reads genuinely Riviera with the harbor umbrellas beyond).
- Restaged 5 Casino Square NPCs off the hero sightline — and the very first plaza screenshot after the restage caught the red parade F1 crossing the square (p6-plaza).
- Grid cars aligned onto the painted grid slots; colliders moved to match.
- Pool diving-tower railings + ladder; grandstand canopy underside light strips (night).
- p6-night-stand: view from inside the blue fan section across the floodlit pit lane — sponsor banner readable, all six garages lit with cars visible. Best night frame so far.

## Pass 7 — 2026-07-05 (closing pass)
Final full-circuit walk on the shipping file: all 10 areas reached on foot, 0 failed waypoints, 61 fps, zero console errors.

**Kept:**
- Start screen now sits over the live, slowly-orbiting golden-hour harbor behind frosted glass (translucent radial scrim + backdrop blur) instead of a flat gradient card (p7-startscreen). HUD hidden until entry — it was bleeding through the frosted overlay.
- Subtle CSS vignette over the viewport — pulls the eye to center in every frame.
- Presence: walking head-bob (speed-scaled, stronger when running) + procedural footstep ticks synced to the bob cycle (louder when running). Audio code-verified, not auditioned (headless).

## Directed pass — 2026-07-05 (user brief: sunset anchor, smooth cars, LOD humans, minimap)
59–64 fps, zero console errors. Grandstand stairs + garage entry re-verified on foot.
- Day-night cycle re-anchored: clock now ping-pongs 16:15 ↔ 20:33 (golden hour → glowing dusk, never midnight). Dusk keyframes keep hemi ≥ .4 and a warm horizon; verified visually at 17:14 / 18:25 / 19:00 / 20:17 (f1-golden, f1-car, f1-dusk).
- F1s rebuilt with continuous curves: lathe nose (first version was inverted + 1.5 m long — caught in screenshot, fixed), capsule tub/engine cover, ellipsoid sidepods, rounded capsule wing elements; MeshPhysicalMaterial clearcoat paint, carbon-weave wings/floor/halo/hubs, saturated liveries. Supercars got clearcoat too.
- Humans: two-tier LOD (45 m switch, zero-scale trick on paired InstancedMeshes — verified numerically both directions). Hi tier: lathe gowns with waists, tapered bent arms, suited men with legs/shoulders/chest, rounded heads + hair caps. Distant tier: original silhouettes; crowd re-blobbed with capsule torsos. Fixed an InstancedMesh frustum-culling bug (stale bounding sphere hid all bodies — floating heads screenshot).
- Minimap: bottom-left live map (track spline, harbor/pool water, player heading arrow, both parade-car dots) → click or M expands to a labeled full-track overlay with a close button; click/× collapses. Verified expand + collapse via real DOM clicks.

## Directed round 2 — 2026-07-05 (keybinds, movement feel, liveliness, kerbs, reflections)
75 fps day & dusk, zero console errors, full circuit re-walked (10 areas, 0 fails).
- Keybinds: Tab jumps straight to the expanded map (Tab/Esc closes), M shows/hides the corner minimap, R resets to the start line. All verified with real key events; pause overlay suppressed while the big map is open.
- Movement: velocity-based accel/decel (no instant start-stop), smoothed mouse look, asymmetric jump gravity (lighter up, heavier down), landing dip, walk-cycle roll.
- Liveliness: NPC weight-shift sway + slow head turns with dwell (hair rotates with head; mannequins stay still), ~40 grandstand fans bouncing and waving instanced arms in their section colors, gulls 4 → 7, dusk tail-light breathing on parked supercars.
- Kerbs: red/white apex kerbs generated from the track spline at 14 corners (Ste Dévote, Massenet, Casino, Mirabeau, hairpin, tunnel exit, Nouvelle Chicane, Tabac, Piscine ×2, Rascasse, Anthony Noghès), inside edge derived from curvature sign.
- **Major bug found by this work: the track ribbon's triangle winding faced downward, so the asphalt had been backface-culled — invisible — since the very first build.** The paved streets had masked it. Fixed with DoubleSide + raised ribbon/kerbs/grid decal above the plaza slab. The circuit now reads as a real racetrack everywhere.
- Graphics: planar Reflector under a now-semi-transparent water shader (yachts/buildings/sky genuinely mirror), 4096px shadows with a player-following frustum + normalBias, facade textures gained balcony rails + striped awnings + warmer window light, 3D balconies/awnings on the hotel, color-grade pass (saturation/warm tint/contrast) in the dusk composer, composer engaged earlier (lightsF > .5).

## Loop pass 8 — 2026-07-05 (expanded brief: race field, living crowds, fast travel)
62 fps, zero console errors, full circuit re-walked (10 areas, 0 fails).
- **The race**: 8 F1 cars in team colors lap the circuit simultaneously with staggered spacing, per-car lane offsets, and phase-shifted speed oscillation (verified: cars covered 22.7 m vs 25.4 m in the same 1.2 s — gaps genuinely open and close, never collide). Static grid cars retired; the positional engine voice now follows the nearest of the 8.
- **Sponsor liveries**: every racer carries four decal panels (sidepods + rear-wing endplates) with fictional sponsors — Riviera Bank, Azur Jets, Chrono d'Or, Monarque, Oro d'Azur, Lumière, Côte Café, Mistral Air.
- **Living pedestrians**: 12 figures now stroll patrol routes (promenades, plaza, pit lane, boutique row, even up the avenue ramp — groundAt keeps them on the slope) with step-bob, forward lean, and direction-facing flips; 8 seated figures occupy benches; standing figures keep their sway/head-turns.
- **Fast travel**: clicking anywhere on the expanded map teleports there and closes the map; harbor/pool keep-out clamps water clicks to the nearest quay (verified: a click on the pool basin landed on the deck edge at exactly the clamp margin). Hint caption added to the big map; × button and small-map-click behaviors preserved.
- Graphics: worn rubber racing line down the circuit center, catch fencing on the pit wall + Ste Dévote, anisotropic filtering on the track texture. Minimap now tracks all 8 cars in team colors.

## Loop pass 9 — 2026-07-05
63–65 fps, zero console errors, full circuit re-walked (10 areas, 0 fails).
- **Ferris wheel** on the east promenade: glowing amber rim, 8 upright colored cabins, slow rotation — a genuine landmark silhouetted against the sunset (r4-ferris).
- **Harbor tender**: small motorboat with driver + fading wake cruising an elliptical loop between the yachts and buoys; verified 6.9 m covered in 2.5 s on-path.
- **Lamp halo sprites**: soft additive glow billboards on all 22 street lamps, opacity tied to dusk — the promenades now bloom warmly at night (r4-dusk-prom).
- **Racers**: blinking red F1 rain lights (shared material, 9 Hz duty-cycle flash); sponsor decals enlarged ~30% + a fifth decal on the nose deck.
- **Café patrons**: three seated figures on stools at the kiosk tables.
- Tuning from side-by-side comparison: dusk color grade softened (sat 1.24 → 1.15, warm tint reduced) after the 19:47 frame ran hot-red; lamp light-pool discs dimmed (they were the "mystery cream quad" when standing on a lamp position). Time ping-pong observed working (clock ran 20:26 → 20:13 between frames).

## Loop pass 10 — 2026-07-05 (race-reactive world)
63–73 fps, zero console errors, spawn→pits walk 0 fails (no collider changes).
- **The world reacts to the race**: `raceExcite` (nearest racer's distance to the grandstand) drives the crowd — cheering frequency and bounce amplitude spike when the field passes, and the audible roar swells with it when you're near the stands.
- Start-light gantry now runs a countdown sequence every ~14 s: five red pods illuminate one by one, hold, then cut — pure race-weekend theatre over the S/F straight.
- Hand flags (Monaco red, white, team blue/orange) waving in the fists of six cheer fans; racers gained soft headlight nose glows that pop in the tunnel dark.
- String lights on the AURELIA (stern → mast → bow catenaries, 24 bulbs, dusk-lit); kneeling mechanic with wheel gun working a crouch cycle beside the Papaya GP garage car (r5-mechanic).
- **Bug found via screenshot**: the garage back-wall team screens had swapped axes since pass 1 — 4 m deep × 0.15 m wide, rendering as a floating color sliver. Fixed; they're proper glowing wall panels now.
- Bottom hint bar updated to teach Tab / R.

## Loop pass 11 — 2026-07-05 (ride the wheel)
63 fps, zero console errors, full circuit re-walked (10 areas, 0 fails).
- **Ride the Ferris wheel**: press E within 15 m to board a cabin, E to hop off. Verified numerically (boarded, tracked cabin altitude 18.2 → 3.3 m through a descent arc, exited at the base) and visually — the view from the top at golden hour is the best establishing shot in the project (r6-wheelview): blimp overhead, a racer in the chicane below, the whole harbor. Contextual "E — ride / hop off" prompt.
- **Sponsor blimp**: RIVIERA BANK airship with fins, gondola, and double-sided banner drifting a slow 125 m circle at 84 m altitude.
- **Pool swimmers**: three figures doing slow laps with alternating stroke splashes and direction flips (r6-swimmers).
- **Screenshot-catch #4**: the pool basin has been sealed by the ground plane since the pass-1 ground rebuild — I cut the harbor hole but never a pool hole; the deck opening sat over solid ground. Fixed by splitting the south ground plane around the basin. The pool has water for the first time since pass 1.
- Tuning: crowd colors deepened (L .33–.53) and floodlight spots eased 900 → 740 to fix the washed-out stand under low sun; E added to start-screen controls.

## Loop pass 12 — 2026-07-05 (event spectacle)
76 fps, zero console errors, spawn→pits walk 0 fails (no collider changes).
- **Jumbotron** on the pit-building roof: a live canvas screen cycling MONACO GP · LAP n/78 · P1 leader (sponsor names rotate), redrawn every 2 s — reads crisply from the grandstand over the team garages (r7-jumbo).
- **Fireworks over the harbor** once the race lights are on (lightsF > .6): three staggered shots on a 5.2 s cycle — rocket rise, 44-particle spherical burst with gravity droop and fade, gold/red/teal. First iteration's particles were invisible specks at 60 m (screenshot comparison caught it); scaled ×3 and now they read as golden rain over the water (r7-fireworks).
- Incidental frame: a racer passing within metres of the camera on the pit straight with the catch fence, banners, and start-light countdown all live — the trackside experience is genuinely eventful now.

## Loop pass 13 — 2026-07-05 (live pit stops)
71 fps, zero console errors, spawn→pits walk 0 fails.
- **Live pit stops**: car 8 periodically (every ~70–120 s) peels off the S/F straight, drives the pit lane at limiter speed along an 8-waypoint path, stops on a freshly painted pit box outside the garages for 8 s, then rejoins the circuit at the pit exit. The existing crew NPCs and kneeling mechanic sit right beside the box.
- Refactored the race from closed-form positions to per-car progress accumulators to allow the mode switch (spacing math re-checked: relative oscillation ±142 m < 163 m car spacing, still collision-free).
- Verified numerically twice: car 8 held stationary at exactly (−152, −24) — the box decal — then correctly appeared at the pit-exit rejoin point. The stop was originally 4 s; stretched to 8 s so spectators (and screenshots) can actually catch it.
- Honest note: the hero still of the stopped car kept losing to the ~1–2 s screenshot round-trip; the pass ships on numeric verification + pit-lane atmosphere frames (r8-pitstop shows the lane with a racer flashing past the grandstand fence beyond).

## Loop pass 14 — 2026-07-05 (crew swarm + Mexican wave)
63–69 fps, zero console errors, spawn→pits walk 0 fails.
- **Pit crew swarm**: four orange-suited crew stationed beside the pit box rush to surround car 8 when it stops (front wing / rear / both sides), crouch-work with staggered rhythm, and retreat to their marks when it leaves. Verified deployed mid-stop in-frame (r9-pitcrew); the car itself hid behind a crew member from my camera spot — three passes of pit-stop stills have now lost to occlusion or latency, while the numerics pass every time.
- **Mexican wave**: every 30 s a gaussian lift ripples through all ~630 grandstand figures over 5 s (full base-matrix restore afterwards). Caught mid-crest on camera — the red sections visibly standing while the blue section sits (r9-wave).
- Bug fix: the pit-box paint decal was z-fighting inside the pit-lane slab (y .09 vs slab top .12) — invisible since it was added; raised above the surface. Cumulative: window-tiled facades everywhere, night bloom + moon + moonlit water, tiled plazas/promenades, layered lit hillside, race dressing (banners/bridge/grid cars/marshals), living world (2 parade F1s with positional engine audio, helicopter, gulls, buoys, flags, palms, fountain), furnished interiors, start-screen glass. Day 62 fps / night 61 fps throughout.

## Loop pass 15 — 2026-07-05 (quality & stabilization)
62 fps day / 64 fps dusk, zero console errors, full circuit re-walked (10 areas, 0 fails).
- **Dusk ambient rescue**: the 18:00–20:00 window has been the weakest-looking hour since the sunset rework — foreground crushed to near-black while the sky stayed pretty. Two rounds of hemisphere/exposure lifts (h18.8 hemi .40→.54, h19.8 .42→.51, h20.6 .46 + exposure 1.05, night hours .45/1.04). Screenshot comparison at 18:30 confirms the pit building, sponsor wall, and city backdrop are now clearly readable where they were silhouettes (r10-duskfix); the sky gradient kept its character. Stopping the ambient tuning here.
- **Track surface lift**: asphalt base #33353a → #3b3d45 so the racing line and kerb edges read at all hours instead of merging into shadow.
- **Photo mode**: P toggles the HUD + minimap off/on for clean captures — added to the start-screen controls. Verified both directions via the DOM class.
- Pit stops now every 45–90 s (was 70–120) so a visitor standing in the pit lane actually catches one.

## Loop pass 16 — 2026-07-06 (1:1 track fixes + directed round 3)
121 fps, zero console errors. Big pass driven by user feedback.
- **Cars no longer drive through buildings**: built a `__mc.clip()` debug scan that tests all 700 track samples against every collider. It found (a) a city infill block straddling the Casino climb — cars drove through 15 m of building; replaced with two flanking blocks west of the track, (b) the Casino terrace retaining wall crossing the racing line — split with a gap where the track tops the hill (also makes the climb walkable on foot, verified), (c) the pool diving-platform pillars standing on the chicane asphalt — the whole tower moved to the south deck. Re-scan: 0 tall-geometry hits within 3.5 m of the racing line. (Tunnel wall flagged too but was a false positive — asphalt correctly meets the tunnel wall.)
- **Drivers in every car**: shoulders + team-colour helmet with dark visor under the halo, merged into the existing paint/carbon geometry so racers, parade cars, and garage cars all get one for free (r12-driver: Papaya GP car with driver clearly seated).
- **Pit crew scaled to human size**: the 4-man swarm rebuilt from 1.2 m mannequins to 1.72 m figures with legs, arms, and white helmets with visors — now matches street NPCs stood side by side (r12-crew-scale). They also turn to face where they're going, and face the car while working.
- **Fluid walkers**: route pedestrians now ease in/out of each leg (smoothstep) instead of hitting the turnaround at full stride, smooth-rotate through the 180° turn instead of snapping, and roll step-synced with their bob.
- **Map cursor fix**: opening the big map (Tab or click) releases pointer lock so the cursor is visible, with a crosshair over the map; closing re-grabs the mouse. Verified: Tab opens → cursor free, Tab closes → relock requested.
- **Skyline pass**: 8-tint Mediterranean palette across the 380 hillside apartments, ~340 rooftop water tanks/AC boxes breaking the flat rooflines, and a fogged mountain-ridge silhouette (Tête de Chien) behind the city (r11-skyline vs r10; r12-ridge is the night-harbor hero shot).
- Also: inline data-URI favicon kills the console 404.
- Ops note: a 2 fps scare turned out to be a corrupted GPU state in a stale Playwright browser instance — bisected my own edits first (both innocent), then a browser restart restored 121 fps.

## Loop pass 17 — 2026-07-06 (racing dynamics + café life)
121 fps, zero console errors, spawn walk 0 fails.
- **Cars now brake into corners and accelerate out**: precomputed a per-sample corner factor from track curvature (smoothed, floor .45); each car's progress rate scales by it, so the field accordions realistically — verified numerically: a car sampled at 4.2 m/s deep in a corner accelerating to 14.7 m/s on exit. The phase-shifted spacing math keeps the field collision-safe (163 m gaps vs ~50 m worst-case compression).
- **Brake lights**: per-car rear brake bar (own emissive material, outside the shared night-light system) with three states — off on straights, 1.1 trail-brake mid-corner, 3.5 hard-braking when the corner factor ahead drops. Verified numerically across three cars: all cycle 0 → 1.1 → 3.5 while lapping. (Three screenshot ambushes at the braking zone lost to latency/occlusion — the numerics are the proof, same conclusion as passes 13–14.)
- **Café de la Rascasse now has a crowd**: three more seated patrons (both sides of each table) and a waiter shuttling kiosk ↔ tables on a short route (r13-cafe: two patrons under the red umbrella, waiter mid-stride).
- Debug: `__mc.race(i)` exposes per-car brake intensity + track position for future verification.

## Loop pass 18 — 2026-07-06 (asphalt rescue + more flags)
121 fps, zero console errors, spawn walk clean.
- **The track no longer reads as a black void**: added a faint fixed emissive (0x232630 @ .42) to the asphalt material. Root cause: the world lives on a dusk↔night ping-pong cycle by design, so the sun never gets high enough for the rough dark surface to catch meaningful diffuse light — every recent screenshot showed pure black asphalt. Side-by-side at the tunnel-exit chicane: before (r14-asphalt-before) the surface is featureless black; after (r14-asphalt) it's charcoal with visible texture, sheen, kerbs, and the racing line.
- **Killed a change that didn't earn its keep**: tire-skid ribbons in every braking zone (reusing the pass-17 corner factor). Implementation was correct, but near-black rubber on near-black asphalt is invisible at every hour this world actually renders — six vantage attempts confirmed it. Reverted in full; the brake lights + accordion remain the braking tell.
- Grandstand hand-flags 6 → 14, colours cycling Monaco red/white/blue/orange.
- Lesson recorded: positive pitch in `__mc.tp` looks UP — several missed vantages this pass were aim error, not world error.

## Loop pass 19 — 2026-07-06 (harbor market)
120 fps, zero console errors.
- **Harbor market on the east promenade**: the plaza between the café and the pool was a barren tiled plain (obvious in r13-cafe). Now: five wooden stalls with individually striped awnings (terracotta, teal, gold, bordeaux, navy), colourful goods crates on every counter, and four stone hedge planters segmenting the space. Each stall is solid — verified the test walker cannot pass through them.
- **Two browser routes** thread walkers through the market gaps (route lines checked against every stall/planter footprint before committing — the first draft would have marched a pedestrian straight through a stall).
- Placement safety: sampled all 8 racers for 15 s before building — nearest approach to any stall spot is 20 m, so the market can never intersect the race.
- r15-market: red/white stall in the foreground with goods, more stalls + planters behind, browsers in frame, tinted skyline + ridge backdrop.

## Loop pass 20 — 2026-07-06 (boutique life + ridge softening)
121 fps, zero console errors, Boutique Row walk clean.
- **Window shoppers at the designer boutiques**: four figures stood right at the vitrines (noses to the glass, properly facing the windows — place() now honours a fixed `ry`), one per shop in gowns/suit that pop against the dark facades (r16-shops: orange gown at ÉLYSÉE, pale pink at MAISON NOIR). The four in-store assistants remain inside.
- **Accent awnings** over every vitrine in the shop's brand colour, tilted off the facade for depth.
- **Mountain ridge softened**: the backdrop peaks read as two stark pyramids in r15. Now 12 overlapping cones (was 7), 1.7× wider, 15–30 % lower, 9-sided — the skyline ends in a rolling ridge instead of triangles (r16-ridge, same vantage as r15-market for comparison).

## Loop pass 21 — 2026-07-06 (paving warmth + corner marshals)
121 fps, zero console errors, Tabac walk clean.
- **Ground paving rebuilt**: the harbor-level promenade tiles read washed-out pale in every wide shot. New palette is deeper Mediterranean sand (6 tints around #a39472), stronger grout lines (3 px, darker), occasional terracotta-stained tiles, and more speckle. Every promenade/market/plaza frame now has a warm, grounded floor instead of a white void (r17-paving vs r15/r16).
- **Corner marshal posts** at Tabac, the tunnel-exit chicane, and the pool complex: white podium (solid, collides), two orange-suited marshals, chrome pole with yellow caution flag (r17-marshal). A fourth candidate spot at Ste Dévote was dropped — 25 s of racer sampling showed the field passes within 6.3 m there, which is on the asphalt edge; the three kept spots clear the racing line by 5 m beyond track width.

## Loop pass 22 — 2026-07-06 (pit-wall gantries)
121 fps, zero console errors, full pit-lane walk clean past both gantries.
- **Pit-wall engineer gantries**: two elevated stands on the pit wall (z −8 and −38) with framed platforms, three glowing timing screens each (canvas-drawn coloured timing bars), and three seated engineers per stand in team colours — the classic F1 pit-wall silhouette. Placement checked against the car-8 pit path (1.7 m clearance) and the second stand moved off a pit-crew home position it would have swallowed. r18-pitwall: gantry screens glowing at dusk, human-scale crew and a spectator in red in the lane, lit hillside behind — one of the strongest frames yet.
- **Marshals got arms** — the pass-21 close-up showed armless boxes; all three corner posts now have properly proportioned figures.
- Bonus catch in r18-garage-driver: the cockpit driver clearly visible in the Monarch F1 garage car.

## Loop pass 23 — 2026-07-06 (take a seat)
Zero console errors; sit/stand verified at all three spots.
- **You can now sit down**: E takes a seat when near one — a new wooden bench on the east promenade (facing the harbor), a café chair at La Rascasse, and a grandstand seat four rows up among the crowd. Movement keys or E stand you back up. The contextual prompt reuses the ride UI ("E — SIT · GRANDSTAND SEAT" / "E — STAND UP"); the Ferris wheel keeps priority when you're near it.
- The grandstand seat is the headline: you sit shoulder-to-shoulder with spectators, looking across the track at the sponsor wall, the team garages, and the live jumbotron (r19-seat). First draft sat you in the front row where the stand's own front wall hid the track — caught via the POV screenshot and moved up to row 4 with a safe stand-up exit at the aisle (verified walkable after standing).
- New geometry: promenade bench (seat, back, legs) + café chair.

## Loop pass 24 — 2026-07-06 (TV broadcast rigs)
121 fps, zero console errors.
- **TV camera crane at Ste Dévote**: base, tower, 14 m boom with counterweight and camera head, slowly sweeping ±24° over the corner (animated via a shared tvRigs list in animateLife). r20-crane caught it with a racer passing under the boom — pure race-weekend broadcast energy.
- **Two panning camera platforms** on the casino terrace balustrade: scaffold towers with rails, tripod-mounted cameras, and a blue-jacketed camera operator each; the rigs pan slowly side to side. Both spots verified 22 m+ from the racing line before building (a third candidate at 6.4 m was dropped).
- All rig bases are solid — the player can't clip through them.

## Loop pass 25 — 2026-07-06 (social life)
121 fps, zero console errors.
- **Conversation clusters**: four groups (pairs and trios, mixed gowns/suits) placed in rings facing each other on the promenade, the market, and Casino Square — the crowd finally reads as people talking, not strangers scattered at random angles. The existing head-turn animation makes them glance around mid-conversation for free (r21-chat: three gowns + a suit in a circle at golden hour).
- **Balcony spectators**: six figures standing on the Hôtel Riviera balconies watching the promenade below (r21-balcony). The verification screenshot caught two of them floating between balconies (upper-row x-coordinates missed the slabs) — fixed before shipping.

## Loop pass 26 — 2026-07-06 (yacht party + braking boards)
121 fps, zero console errors, AURELIA deck still walkable through the party.
- **Party on the AURELIA**: five guests on the hero yacht's aft deck — four in a circle around a new champagne table (white top, chrome leg, ice bucket) and one woman in red at the rail gazing over the harbor. Under the existing mast string lights at dusk it's the glamour brief in one frame (r22-party: guests, glowing table, blimp, moonlit sky, lit hillside).
- **Braking-distance boards**: red-and-white 100/50 boards on posts counting down to Ste Dévote, facing oncoming cars (r22-boards, with the TV crane sweeping behind them).

## Loop pass 27 — 2026-07-06 (defect sweep: NPC dusk readability)
121 fps, zero console errors.
- Ran a fresh-eyes sweep of four areas (tunnel / pool / casino / approach). The tunnel is genuinely cinematic now — r23-tunnel caught the Monarch car with its driver's helmet framed by the glowing portal arch. The systemic defect found: **dark-suited NPCs crush to featureless black silhouettes at dusk** (r23-npc-before) — same root cause as the pass-18 black asphalt, since this world permanently lives between golden hour and night.
- Same cure applied: faint warm emissive on both NPC cloth materials, the hair material, and the bench-sitter material (intensity .4–.45 after a first pass at .24 proved invisible in a side-by-side), plus the darkest suit colours lifted (e.g. 0x14161c → 0x272a33). Figures now keep shoulder/arm/hair definition when backlit while staying appropriately dusk-dark (r23-npc-lift).
- Walk-check note: a "failed" casino walk turned out to be the test teleporting into the fountain's collider — correct blocking, not a regression; the offset path walks clean to the conversation cluster.

## Loop pass 28 — 2026-07-06 (pool glow)
121 fps, zero console errors (custom shader edit — verified compiles clean).
- **The pool glows after dark**: added a uGlow/uGlowCol channel to the shared water shader — night blend toward luminous turquoise with a slow caustic-style shimmer — enabled only on the pool water (harbor unchanged), plus two aqua point lights that ramp with the existing lightsF system, washing the deck. The sweep-pass near-black basin (r23 era) is now the night-time centrepiece of the pool complex (r24-poolglow: glowing pool, swimmers, lit deck, city + jumbotron behind).

## Loop pass 29 — 2026-07-06 (victory podium)
121 fps, zero console errors, podium collider verified (walker stops at its edge).
- **Victory podium on Casino Square**: gold-trimmed "GRAND PRIX DE MONACO" sponsor backdrop on posts, wine-red 2-1-3 steps with gold numeral plates and gold step edging, a race-suited winner on the top step with arms up and a glowing champagne spray, and the trophy on P2 (r25-podium, lamp-lit at dusk). Site chosen at (40,−145) after sampling the field for 25 s — 31 m clearance from the racing line.

## Loop pass 30 — 2026-07-06 (exhaust glow + full-circuit regression)
121 fps, zero console errors.
- **Exhaust glow on the racers**: each car has an exhaust that flares orange on corner exit and dims under braking, night-gated by the streetlight system. Verified numerically: intensity sweeps 0.3 → 2.2 across 58 distinct sampled states while the field laps after dark — it breathes with the throttle.
- **Full-circuit walkability regression** — first comprehensive walk since pass 16, covering 14 passes of added colliders (stalls, marshals, TV rigs, pit gantries, podium, seats, planters). 19 walk legs run. Every apparent failure investigated and confirmed as a *legitimate* obstacle, not a trap: the pit wall (enter the pit lane via its ends), a market stall on the direct diagonal (gaps walk fine), the yacht hull (gangplank walks fine, deck y 1.6), the pool basin rim, the casino fountain (photographed — r26-casino-fountain), and the casino building itself. Pit entry, market gaps, gangplank, pool north deck route, terrace climb crossing, boutique row, and the full tunnel all walk clean.

## Loop pass 31 — 2026-07-06 (tender wake + start screen)
120 fps, zero console errors.
- **Foam wake behind the harbor tender**: a ring buffer of ten fading foam discs dropped at the stern every .32 s, expanding and fading over ~3 s. First version was invisible — the discs rendered under the transparent water plane's forced render order; fixed with renderOrder 2 + raised to just above the surface. Honest note: four camera attempts failed to frame the moving boat itself (the same latency battle as the racers — logged and conceded to live play; the code path runs clean and the discs sit correctly above the waterline).
- **Start screen controls updated** — E now documents both the Ferris ride and sitting on benches/stands.
- Incidental keeper: r27-yacht-bow — the AURELIA bow from water level with the party guests visible on deck, city reflections all around.

## Loop pass 32 — 2026-07-06 (start-screen backdrop)
120 fps, zero console errors, game starts cleanly at the harbor spawn.
- **Intro camera relocated**: the start-screen backdrop had panned across a drab dark quay corner since the early passes. It now floats 13 m above the pool-chicane promenade, slowly panning across the pool deck, moored yachts, palms, the Monaco flag, and the hillside city (r28-intro-before vs r28-intro-after) — the first thing a visitor sees is now the world at its richest.
- Start-screen controls text already refreshed last pass; verified the new backdrop keeps the overlay text legible (dark blur layer unchanged).

## Loop pass 33 — 2026-07-06 (map points of interest)
122 fps, zero console errors.
- **POI markers on the fast-travel map**: seven gold dots with labels — MARKET, PODIUM, FERRIS WHEEL, CAFÉ, CASINO, YACHT AURELIA, FOUNTAIN — so the Tab map now advertises where the good stuff is instead of assuming you know (r29-map, with the live race dots and player arrow also in frame).
- Verified end-to-end: clicked the MARKET dot on the expanded map → player landed at (77, 65) beside the stalls and the map closed itself.

## Loop pass 34 — 2026-07-06 (paparazzi)
121 fps, zero console errors.
- **Paparazzi at the podium**: three dark-suited photographers ring the victory podium, cameras raised at the winner (r30-paparazzi). Each has a white flash plane that pops for 0.13 s on its own 2.2–4.2 s cycle, driven from the life loop — at night the podium corner now sparkles with camera flashes. (No still caught a flash mid-pop — a 0.13 s window defeats screenshot latency by design; the animation one-liner follows the same verified pattern as the TV-rig pans.)

## Loop pass 35 — 2026-07-06 (supercar headlight pools)
121 fps, zero console errors, boutique street walk clean.
- **Headlight pools for the parked supercars**: each of the seven has an additive warm-white ellipse on the pavement ahead of its nose, aligned to the car's heading and ramping with the streetlight system (15 % of lightsF). r31-scpools: the red supercar outside the boutiques with its beam washing the pavement, window shoppers at the lit vitrines behind — the luxe night-shopping-street look the original brief asked for.

## Loop pass 36 — 2026-07-06 (chicane fans)
121 fps, zero console errors.
- **Trackside fans at the pool chicane**: found the circuit's slowest point empirically (sampled all 8 cars for 20 s — minimum 4.7 m/s at the chicane) and placed two fan clusters against the barriers there, where real Monaco crowds press in. Safety sampling rejected two candidate spots outright — one had cars passing 0.9 m away (on the racing line), the other 5.9 m; the two kept spots clear by 15–18 m. r32-fans: spectators at the barrier with the track, Monaco flags, and the city bowl behind.

## Loop pass 37 — 2026-07-06 (the Prince's Palace)
120 fps, zero console errors.
- **Le Rocher**: the Prince's Palace now stands on a rocky headland southwest of the bay — crenellated wall with nine merlons, twin square towers with terracotta pyramid roofs, a keep with the red Monégasque flag, and warm windows that light at dusk. First placement sat too low and vanished behind an intervening structure from every harbor angle (two comparison shots confirmed it); raised the mesa to 48 m so the silhouette clears the rooftops as the real one does. r33-palace: the palace on its rock beside the setting sun, seen across the pool with the helicopter overhead — the southwest horizon finally has its landmark.

## Loop pass 38 — 2026-07-06 (safety car + old town)
121 fps, zero console errors.
- **Safety car** parked behind the garages at the pit exit: silver, glowing orange roof light bar, headlights washing the pavement, SAFETY CAR livery on the flank (r34-safety — against the lit hillside at night).
- **Old-town houses on Le Rocher**: eight small terracotta-roofed houses climb the rock below the palace, so the headland reads as Monaco-Ville rather than a bare mesa (r34-rocher: palace + houses over the rooftops with a racer passing the pool chicane below).

## Loop pass 39 — 2026-07-06 (west hill fix + grounded houses)
121 fps, zero console errors.
- **Identified and fixed the giant blank slab** that has dominated the southwest of many frames since early passes: it's the west hillside box, which rendered as featureless beige concrete. Both hill materials (near + far) now carry a mottled Mediterranean-scrub canvas texture — the whole backdrop reads as vegetated hillside (r35-hill-before vs r35-hill-after).
- **Floating-house bug fixed**: yesterday's old-town houses were placed at fixed heights on a circle that missed the mesa cone's surface — several hovered in mid-air (caught in the before shot). They're now snapped to the actual cone-surface height at their radius, hugging the rock just below the palace.

## Loop pass 40 — 2026-07-06 (confetti + mesa rock)
121 fps, zero console errors.
- **Confetti over the podium**: seventy instanced paper pieces in gold/red/white/blue flutter-fall over the ceremony — sinusoidal drift, tumbling rotation, respawn at the top — completing the celebration stack: winner, champagne spray, paparazzi flashes, now confetti (r36-confetti, with two paparazzi heads framing the shot).
- **Mesa rock texture**: Le Rocher's smooth grey cone now carries a mottled rock canvas texture, matching last pass's scrub hillsides.
- Ops note: second occurrence of the 2 fps Playwright browser degradation mid-verification — browser restart restored 120 fps, confetti code confirmed innocent. Pattern noted: the test browser decays after long sessions; not a world bug.

## Loop pass 41 — 2026-07-06 (quay foam + perched gulls)
121 fps, zero console errors.
- **Lapping foam along the quay walls**: four pale strips hug the harbor's quay bases, opacity breathing on a slow sine so the water edge laps rather than meeting the wall in a hard line (r37-foam: the strip receding along the brick quay wall).
- **Perched gulls**: two gulls (body, folded wing, yellow beak) sit on actual promenade bollards. First placement floated in mid-air — I'd guessed bollard positions instead of reading them; the bollard rows are at z 61.6, not the quay lip. Snapped to real bollards at the correct cap height (r37-gull, with a flying gull's shadow passing nearby).

## Loop pass 42 — 2026-07-06 (casino floor + doorman)
121 fps, zero console errors.
- **The casino has players**: a croupier behind the roulette wheel and two guests — red gown and midnight suit — stood at the green-felt table under the chandelier (r38-casino, shot from inside the wine-red lobby). The enterable interior finally has a reason to enter.
- **Doorman** posted under the Hôtel Riviera entrance canopy.

## Loop pass 43 — 2026-07-06 (fluttering flags)
119 fps, zero console errors.
- **The marshals' yellow flags and the palace flag now flutter** — a shared waveFlags list drives a ±23° breeze oscillation from the life loop. Verified with two frames a second apart: the Tabac marshal's flag twists from edge-on to full-face between them (r39-flag-a / r39-flag-b). Small touch, but static flags read as toy props; moving ones read as weather.
- (Declaration-order lesson re-applied: the shared list had to be hoisted to the top of the file — the first placement sat after the marshal code and would have hit the same TDZ error as pass 16's pointer-lock fix.)

## Loop pass 44 — 2026-07-06 (guided tour)
121 fps, zero console errors.
- **Guided tour mode**: press G and the world chauffeurs you through ten curated vantage points — start gantry, pit-wall gantry, yacht party, market, café, glowing pool, podium, boutiques, tunnel, palace view — eight seconds each, looping. Any movement key (or G) hands control back; the prompt bar explains ("G — END TOUR · ANY KEY TO EXPLORE"). Verified end-to-end: three stops visited at the exact scripted coordinates on the 8 s cadence, prompt correct, clean exit, zero errors. Added to the start-screen controls.
- r40-tour: the café stop mid-tour — waiter, patrons, market, palace, and blimp in one frame. This is the show-off feature for handing the file to someone: click once, press G, watch.

## Loop pass 45 — 2026-07-06 (tour polish + regression audit)
121 fps, zero console errors.
- **Cinematic tour pan**: while the tour holds at each stop, the camera now drifts slowly (2.6°/s) instead of freezing — each vantage becomes a gentle establishing shot.
- **Regression audit after 14 build passes**: track clip scan returned 152 hits — identical to the pass-30 baseline (all known viaduct supports and trackside barriers; zero new intrusions from the market, podium, TV rigs, gantries, palace, or seats). All ten named areas teleport-reachable at correct ground heights (0 harbor level / 6 terrace level). r41-tunnel-stop: the tour's tunnel stop, kerbs sweeping to the glowing portal.

## Loop pass 46 — 2026-07-06 (overtaking)
120 fps, zero console errors.
- **The race has real overtakes now**: odd-lane cars carry a .35 m/s pace advantage, so they systematically reel in and pass the even-lane cars — always on the opposite side of the road (odd/even lane offsets have opposite signs), so every pass is a side-by-side moment rather than a same-line overlap. Verified numerically: the arc-gap between cars 0 and 1 swung from +86 m to −73 m in a 30 s window — a genuine position swap on the clock. The pass-17 corner accordion turns out to have created latent passing chances already; the pace delta makes them systematic. Same-parity (same-lane) cars carry identical speed, so their spacing behaviour is unchanged — no new overlap risk.

## Loop pass 47 — 2026-07-06 (live race leader)
120 fps, zero console errors.
- **The jumbotron P1 is now real**: cars count laps as they cross the line, and the big screen shows the sponsor name of the car genuinely furthest around the race — so when an overtake for the lead happens (possible since pass 46), the board updates within its 2 s redraw. Previously P1 was a name cycling on a 15 s timer.
- **Leader ring on the map**: the fast-travel map's race dots now draw a gold ring around the actual leader (r42-leader). Both displays share the same four-line max-progress loop.

## Loop pass 48 — 2026-07-06 (scoring pylon)
121 fps, zero console errors.
- **Monaco scoring pylon at the start/finish straight** (−127.5, 24): a 10.4 m black tower with a live P1-P8 leaderboard, redrawn every 2 s from the same real race progress (laps × trackLen + arc position) that drives the jumbotron — gold position numbers, per-car team colour bars, three-letter codes (RIV/AZJ/CHR/MON/ORO/LUM/CAF/MIS). Overtakes reorder the board live.
- Spot verified safe before building: 20 s of 8-car sampling, minimum 7 m clearance. Collider on the tower; clip-scan baseline unchanged.
- Close-up screenshot caught the face plane embedded 0.2 m inside the tower box (dark band splitting the display) — moved to x −128.06, just off the tower's west face. r43-pylon confirms a clean continuous display.

## Loop pass 49 — 2026-07-06 (sailboats at anchor)
121 fps, zero console errors.
- **Three sailboats at anchor in the basin** at (74,−30), (74,44), (0,−34): white hulls with coloured waterline stripes (navy/claret/green), teak decks, cabins, 8.6 m masts with boom and furled sail, and a warm masthead lamp that comes up with the race lights. They bob, roll, and swing slowly at anchor alongside the buoys.
- First-draft anchor spots all clipped the existing bgYachts (I hadn't audited the moored fleet at (24,−24)/(56,32)/(−12,44)/(60,−2)) — caught it in the first screenshot and re-plotted against every hull's extent plus the tender's cruise ellipse before keeping.
- Also caught and reverted two accidental duplicates this pass before they shipped: a second blimp and a second gull flock (both already exist from earlier passes) — audit-before-build now includes a grep for the feature name.

## Loop pass 50 — 2026-07-06 (player-reactive pigeons)
121 fps, zero console errors.
- **Seven pigeons peck around the Casino Square fountain** — grey bodies, darker heads, amber beaks — with a smooth peck cycle and slow wandering head-turns while idle.
- **They scatter from the player**: walk within ~4.5 m and a pigeon takes off in a smoothstep arc directly away from you (clamped to the plaza, steered off the fountain basin), flapping at 26 rad/s, then lands and goes back to pecking. First interactive wildlife in the world.
- Verified behaviourally twice: approached a pigeon and it relocated to exactly the computed landing spot (clamp boundary x −9), resuming its peck cycle; approaching the new spot scattered it again. The 2.6 s flight is shorter than screenshot latency, so the airborne frame itself wasn't captured — the landing-spot match is the proof.

## Loop pass 51 — 2026-07-06 (working street clock)
121 fps, zero console errors.
- **Ornate double-faced street clock (horloge) on the east promenade** at (84,40): dark-green column, cream faces with hour ticks and a MONACO wordmark, faint face glow for dusk readability, collider on the base.
- **The hands run on the real game hour** — the same variable that drives the sun and the HUD clock. Verified across two times: at 18:12 the minute hand sat at 72° and at 20:24 it had swung to 144° with the hour hand past 8 — both faces mirrored so each reads clockwise from its own side.
- Bonus composition: the night close-up frames the clock against the fireworks, the RIVIERA BANK blimp, and the lit skyline (r46-clock-night).

## Loop pass 52 — 2026-07-06 (dog walker)
121 fps, zero console errors.
- **A dog walker strolls the north promenade** (x −36..36 at z 66.5): owner in a navy jacket with a full stride cycle (scissoring legs, swinging free arm, subtle bounce), leash in the low hand running to a tan dog trotting at heel — diagonal-pair leg trot, wagging tail, ears and snout. They ping-pong the promenade at a stroll (1.6 m/s, slowed from an initial too-brisk 4 m/s) with a smooth turn at each end.
- Route bug caught before shipping: the first route (z 71) ran straight through the CHRONO D'OR show car and the La Piscine loungers — discovered by teleporting onto the route line itself. Re-plotted to the open pavement lane between the bench row (z 64) and the palm line.
- Added `__mc.dogPos()` — chasing a moving subject by guesswork cost five wasted screenshots; the debug getter made the final framing deterministic.

## Loop pass 53 — 2026-07-06 (fireboat salute)
121 fps, zero console errors.
- **A fireboat anchors the empty west basin** at (−50,40): red hull with bow cone, white deck and wheelhouse with a dark glass strip, bronze water monitor on top — bobbing and rolling gently. Spot checked against every water occupant (AURELIA, tender ellipse, four bgYachts, six buoys, three sailboats).
- **Twin water arcs spray from the monitor**: 18 additive-blended droplets per side along a parabola that actually lands in the water, drop scale swelling toward the end like mist, with a travelling pulse (t·9 − k·1.15) that reads as flow. At dusk the arcs catch the light against the lit skyline (r48-fireboat).
- Two iterations to get the arcs right: the first version sprayed 6 m sideways nearly flat — read as a detached bubble trail in the screenshot — and was reshaped to a tight 45° jet; the second pass densified 12→18 drops per arc.

## Loop pass 54 — 2026-07-06 (grandstand camera flashes)
117 fps, zero console errors.
- **Camera flashes ripple across the grandstand after dark**: 40 additive white pops sampled evenly from real crowd seat positions, each on its own 1.3–3.7 s cycle with a 0.16 s pop, gated on the race lights (lightsF > .55) so daytime stays clean. Reads as fans photographing the cars — several flashes visible in any given frame across both colour sections (r49-crowdflashes).
- First version was too sparse (26 flashes × 0.11 s ≈ one visible per frame — invisible in practice); density math now targets ~2.6 visible per frame.
- fps 117 vs the usual 121 — within normal variance for this probe, will keep an eye on it next pass.

## Loop pass 55 — 2026-07-06 (jet ski)
120 fps, zero console errors.
- **A jet ski carves continuous circles off the south-east quay** (centre 44,−12, radius 7 m — verified clear of both nearby bgYachts, the tender ellipse, and the sailboats): white hull with red deck, crouched wetsuit rider with a yellow helmet, constant inward lean plus chop-bounce and pitch jitter, and an additive rooster-tail of seven pulsing droplets.
- It's the first fast-moving watercraft — the harbor now has slow traffic (tender), static moorings, and sport. fps back at 120 (last pass's 117 was probe variance, as suspected).

## Loop pass 56 — 2026-07-06 (balloon vendor)
121 fps, zero console errors.
- **Balloon vendor at the foot of the Ferris wheel** (134,101): red-vested figure with a flat cap, one arm raised holding a bundle of eight bright balloons (red/amber/blue/green/magenta/yellow/teal/white) on individual strings that converge to the hand. The whole bundle sways on two slow sine axes; each balloon carries a faint emissive lift so the cluster glows at dusk beside the lit wheel rim (r51-balloons-dusk).
- Close-up review caught the head floating above the shoulders — reseated it flush with the vest, matching the blocky proportions of the world's other figures.

## Loop pass 57 — 2026-07-06 (quay fisherman)
121 fps, zero console errors.
- **A fisherman sits on a crate at the south quay edge** (58,−40.6): green coat, bucket hat, legs dangling over the wall, rod angled out over the harbor with a line dropping to a red float. The float bobs on the chop, and every ~9 s a "bite" pulls the float under while the rod tip flicks down in sync.
- The line initially hung 1.2 m beyond the rod tip (guessed z instead of computing the tip's world position) — moved to sit directly under the tip. A false alarm about the rod pointing inland turned out to be its shadow on the building plus a bad camera angle; a second angle plus the tip math confirmed it correct.

## Loop pass 58 — 2026-07-06 (kids at play)
121 fps, zero console errors.
- **Two kids chase each other around the pool plaza** (circle at −8,82, radius 4.5 m — clear of the pool wall, benches, and the show car): 1.1 m figures in red and blue tees with shorts, fast leg-scissor run cycles, pumping arms, a bounce in each stride, and a slight lean into the turn. The follower trails half a radian behind the leader — a perpetual game of tag.
- First interior-plaza children in the world; the piscine now has sunbathers, swimmers, strollers, and play.
