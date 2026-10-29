# Making the animation belong in the world (37 items)

The user asked (29 Oct 2026) to fix all 37, working until the session limit. Status: `todo`, `doing`, `done`, `later` (needs a bigger build first). Prove each with stills, not full renders.

## The first 7 (T1–T7; renamed from A1–A7 so they don't clash with the checklist's writing items A1–A3)
| # | Item | Status |
|---|---|---|
| T1 | Layers and contact: object fronts in front of the cast (sofa, railing, steps, cattails); sit/stand inside things | done |
| T2 | Depth staging: not one row; nearer = bigger and lower, further = smaller and higher, overlaps | done (spots step back alternately; smaller further back) |
| T3 | Light matches the set: night = blue tint on the cast, warm glow near lamps, sunset side light, rim light | done |
| T4 | The set is alive: water shimmer, swaying grass and trees, fan turning, twinkling lights, fireflies, bobbing duck, drifting clouds | done (fireflies, water glints, twinkling bulbs, dust, plant breeze; fan and clouds later) |
| T5 | Characters use space and props: walk in and out, walk to the steps then sit, paw hits the switch, real hold on chips and phone | done (walk on/off with stride, bob, arm swing, footsteps; porch light switches on, timed to the line; phone in paw). A real paw reaching the switch is still to do: checklist B8 |
| T6 | Characters react to each other: look at the speaker, listeners react, bodies angle toward each other | done |
| T7 | Camera uses the space: wide, medium and close shots, pans and push-ins, layered sets for 2.5D | done (wide/close/two/ots/at shots, push-ins, slow "move" across a beat; 2.5D layers later) |

## The 30 more
| # | Item | Status |
|---|---|---|
| 1 | Shadows change with time of day (short noon, long sunset, none at night) | done (sunset long and sideways, night faint) |
| 2 | Light falloff: further from a lamp = slightly darker | done |
| 3 | Moving light patterns on characters (leaf shadows, lake ripple light) | done ("dapple": leaf shadows at the stoop, water light at the lake) |
| 4 | Atmospheric haze on characters far back | done (spots further back get the set's air colour) |
| 5 | Glints on shiny things (whistle, phone, brass porch light) | done (whistle glint; brass porch light glows with the lamp) |
| 6 | Flashlight cones light only what they touch in dark scenes | done (flashlight beat effect: beam + spot follow a path) |
| 7 | Footprints in the sand | done (prints appear under each step on sand sets) |
| 8 | Dust puffs on jumps, landings, sofa flops | done (dust at the feet on hops, takes and cheers, coloured by the surface) |
| 9 | Cushions squash when sitting | done (a soft hollow under everyone sitting; animated squash on flops later) |
| 10 | Splashes and ripples (duck moving, touching water) | done (the duck bobs with expanding ripple rings) |
| 11 | Leaves and grass react when brushed | later (needs walking through foreground plants) |
| 12 | Reflections in the lake under characters near water | later (no one stands at the water's edge yet) |
| 13 | Idle weight shifts (lean, cross arms, scratch ear) | done |
| 14 | Breathing matches mood (slow calm, fast after a scare) | done (breathing exists; mood-matched speed later) |
| 15 | Sitting poses: slouch, knees up on the step, lying on the beanbag | done for sitting (sofa, beanbag, step; knees apart). Slouching and lying: todo, checklist B6 |
| 16 | Reactions to place: squint in sun, shiver in the hall, fan themselves in the heat | done ("fan" in the heat, "shiver" in cold or spooky places) |
| 17 | Hands really hold props (chips, phone, flashlight, cup) | done ("carry": phone, flashlight or cup in the paw; Riot reads cards off his phone; Rocco's chips) |
| 18 | Eye-lines hit targets (the duck, the porch light, the phone) | done (lines can look at cast or up/down/left/right, e.g. up at the porch light) |
| 19 | Overlapping action: ears, tails, strings follow fast moves | done |
| 20 | Hesitation before actions (before the hall door) | done (line "pause" + face; e.g. a beat before the hall door) |
| 21 | Footsteps change with the surface (sand, wood, creaky boards, pavement) | done (step_wood/sand/stone sounds; used in the cold open) |
| 22 | Room sound per place (hall echo, cosy indoors, open lake air) | done |
| 23 | Sounds tied to visible objects (fan hum, porch-light buzz, door creak, sofa springs) | done (room tones, porch-light click, wooden steps, footsteps, door on exit; sofa springs later) |
| 24 | Voices sound like the space (echo in the hall, whisper at night) | done (hall echo; night whisper later) |
| 25 | Over-the-shoulder shots in conversations | done (camera "ots:a,b") |
| 26 | Point-of-view shots | done (camera "at:px,py,size" for point-of-view / insert shots) |
| 27 | Foreground framing (through cattails, past the railing, between stair bars) | done |
| 28 | Matching cuts: exit right, enter left | done (exit right / enter left with "enter"/"exit") |
| 29 | Establishing shots before each new place | done (beats with an empty cast work as establishing shots) |
| 30 | Time passing in the background (sun lower, windows lighting up, moon moving) | done (the episode moves afternoon to sunset to night; lamp_on lights windows) |

## How to use it in an episode JSON (all opt-in; Shorts and older episodes are unchanged)
| Field | Where | What it does |
|---|---|---|
| `"riot_optional": true` | episode | beats may leave Riot out (not game beats) |
| `"ending": "porch_light"` | episode | porch light clicks off, black, small Friendzy logo |
| `"beds": {"normal": "lofi"}` | episode | lo-fi music for normal scenes |
| `"riot_phone": true` | episode | Riot reads game cards off his phone |
| `"seats": {"bash": "sofa_l"}` | beat | named spots per painted set: `sofa_l`, `sofa_r`, `beanbag` (apartment), `tower` (lake), `step` (stoop), `edge` (hall), or 0–3 standing |
| `"enter": {"bash": "left"}`, `"exit": {"rocco": "right"}` | beat | walk on/off with steps, arm swing, footsteps, footprints on sand |
| `"exit_sfx": "door"` | beat | a sound as the walk off ends |
| `"move": "at:860,200,9.0"` | beat | slow camera move across the beat |
| `"carry": {"riot": "flashlight"}` | beat | phone, flashlight or cup in the paw |
| `"fx": [...]` | beat | `lamp_on` (a light switches on), `flashlight` (beam along a path), `critter` (duck, Lord Puddles; bob, ripples) |
| `"camera"` | beat or line | `wide`, `close:who`, `cu:who`, `two:a,b`, `ots:a,b` (over the shoulder), `at:px,py,size` (point of view / insert) |
| `"look"` | line | a cast name, or `up`, `down`, `left`, `right`, `up_right`... |
| `"do"` | line | existing moves plus `fan` (heat) and `shiver` (cold, spooky) |
| `"face"` | line | also `soft`, `sad`, `embarrassed`, `scared`, `determined`, `asleep` |
| `"quiet": true` | line | small acting, no gestures; the music steps back |
| `"emote": "zzz"` | line | sweat, anger, sparkle, question, exclaim, heart, zzz |
| `"asleep": ["rocco"]` | beat | eyes shut, head tipped, slow breathing, floating z's |
| `"chat": [["Riot", "LIGHT'S ON"], ...]` | beat | group-chat bubbles pop in one by one |
| `"weather": "storm"` | beat | rain, lightning, thunder, darker sky, rain sound |
| `"walk_to": {"riot": ["s3", 2.0]}` | beat | walk to another spot mid-scene and stay |
| `fx` `title` | beat | big title letters popping in (the intro) |
| `fx` `critter` `"poses"`, `"blink"` | beat | switch poses on cue; blink every few seconds |
| `"direct": "auto"` | episode | the auto-director: picks the shots, reaction cuts, who each line is said to, and how hard it's played, wherever the script didn't. Writes `shots.txt` (every camera choice and why) next to the video. Anything the script sets itself wins |
| `"to": "bash"` | line | who the line is said to: the speaker turns to them (the auto-director fills it in) |
| `"energy": 1.25` | line | how big the line is played (the auto-director sets it from the punctuation: "!" 1.25, a SHOUTED word 1.4, "..." 0.8) |
| `"cu:who"` | camera | a real close-up (head and shoulders), framed with room on the side they look toward; `close:` stays the medium shot it always was |
| `fx` `label` | beat | words on the set itself, e.g. `{"type": "label", "text": "12 AUGUST", "at_px": [610, 240], "size": 0.5}` (a calendar page, a sign). Paintings stay free of text; pair it with an `at:` camera for the insert shot |

Set data (spots, front pieces, lamps, life) lives in `art/hd/sets/<painting>.json`; front pieces are cut by `tools/fronts.py`.

More set life (29 Oct), each placed in painting pixels in the set's JSON `"life"`: `clouds {area, n}`, `ripples {area, n}`,
`townsfolk {path: [x0, y, x1], n, size}`, `bike {path, every}`, `stars {area, n}`, `moon [x, y, r]`, `porchlights [[x, y], ...]`,
`dragonflies {area, n}`, `fish {area, every}`, `pollen {area, n}`, `fog {area, n}`, `flicker [[x, y, r], ...]` (a TV's light),
`heat {area}`, `puddles [[x, y, w], ...]`, `wall_shadow: 0.3` (a wall close behind the cast). Nothing shows unless the set lists it.

The episode JSON is checked before anything renders: a speaker, `look`, `target`, `react` or camera name that isn't in the beat's cast, an unknown `do`, `fx`, `carry`, mood, weather or transition, an `enter`/`exit` side other than left/right, or an empty line stops `make.py` with a message saying what's wrong.

The Porchlight folder is found at `~/Desktop/Porchlight`; set `PORCHLIGHT_DIR` if it moves (`BLENDER` likewise points at another Blender).
