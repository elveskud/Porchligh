# Porchlight animation bible: dos, don'ts and the checklist

The reference for making every episode look and move right. Read the rules before scripting, building a set or touching the pipeline.

- **Part 0: the rules (dos and don'ts)**, learned from Episode 1 (28–29 Oct 2026). Add to them whenever something new is learned.
- **Part 1 / 1b: known problems**, with fix ideas, effort (S = hours, M = a day, L = several days), priority (1 = first) and status.
- **Part 2: the per-episode checklist**, to copy for every episode.
- The JSON fields that make all of this happen are listed in `ANIMATION_TODO.md` (bottom). The first 37 items are tracked there too.

---

## Part 0: the rules

### Look and style
| Do | Don't |
|---|---|
| Use the **code-drawn Friendzy cast** (real app designs, already rigged) | Use Gemini cut-out characters (tried 29 Oct: stiff, off-model) |
| Have Gemini paint sets **in the cast's style**: bold black outlines, flat colours, one hard shadow; attach `lake_day_v2` as the reference | Use painterly or sketchy sets (they make the cast look like stickers), or code-drawn sets (tried: too flat) |
| Repaint day/sunset/night as **the same picture** (same composition) | Ask for a new picture per time of day |
| Upscale every painting to **4K** (`tools/realesrgan`, with `-m models`) | Use the 1024 px originals in a render |
| Ask for **no fireflies, light beams, particles or text** in paintings | Let Gemini bake in effects: they sit frozen next to the animated ones |

### Gemini prompting
| Do | Don't |
|---|---|
| Put the **style lock inside every prompt**, and attach the reference images every time | Rely on an earlier message in the chat to hold the style |
| Ask for **one complete sheet per character or prop** | Ask for one part per message (styles drift between messages) |
| Check every cell is a **drawing, not a word** ("OPEN", "(A) MOUTH") | Accept a sheet without checking it |
| Use `art/SET_PROMPT_TEMPLATE.md` for new sets | Write set prompts from scratch |

### Staging: making characters belong in the place
| Do | Don't |
|---|---|
| Sit characters **in** furniture (`sofa_l`, `beanbag`, `step`) and inside things (`tower`) | Line everyone up in front of the furniture |
| Stage in **depth**: alternate front and back spots, overlap a little | Put everyone in one row at one size |
| Bring characters on and off with **walks** (`enter`, `exit`, `walk_to`) | Pop characters in, or jump them to a new spot in the same shot |
| Give every scene **one piece of physical business** (a prop, a walk, an object used) | Write long scenes of four characters only talking |
| Aim eye-lines at things (`look`: the light, the duck, the phone) | Leave everyone staring at the camera (except the deliberate stare gag) |
| Use the duck, Lord Puddles and set life to keep the frame alive | Leave a shot completely still |

### Light and colour
| Do | Don't |
|---|---|
| Light the cast **like the set** (`cast` in `PLATE_SETS`): blue at night, warm at sunset and by lamps | Leave the cast day-lit on a night set |
| Match shadows to the time of day (long at sunset, faint at night) | Use the same shadow everywhere |
| Use `lamp_on` when a light switches on (it warms the whole place) | Add a glow without changing the room |

### Camera
| Do | Don't |
|---|---|
| Vary shots: wide to set the place, then medium, close, `ots`, `at` | Stay on the wide shot for a whole scene |
| Use slow `move`s for moods (the cold open creeping in, the hill at the end) | Cut everything hard and static |
| Trust the frame clamp: cameras stay inside the painting | Frame close-ups past the painting's edge (it shows black) |

### Sound and music
| Do | Don't |
|---|---|
| Give every place its **room tone**; footsteps match the surface | Leave scenes silent under the dialogue |
| Mark emotional lines `"quiet": true` (small acting, the music steps back) | Play an emotional line like a joke |
| Generate everything (voices, sounds, music) | Use licensed music or recorded sound libraries |

### Writing for animation
| Do | Don't |
|---|---|
| Check the JSON features table before writing an action | Write actions the engine can't do yet without flagging them as a build item |
| Put one visual gag in each episode that works with the sound off | Rely on words for every joke |
| Keep Friendzy natural: real games, real prompts (`prompts.py` or the app source) | Invent app UI or prompts, or say "download now" |

### Pipeline and process
| Do | Don't |
|---|---|
| Prove changes with **stills** (`--stills`), then render only approved episodes | Render the full video while still improving (user rule, 29 Oct) |
| Copy `vo/` into a new video folder before using `--reuse-voices` | Start a new `--name` without voices (it regenerates all of them) |
| Render with `--jobs 6` on this Mac (M3, 8 cores) | Use the default 3 jobs |
| Make anything that switches on/off use **CONSTANT** keyframes (`fcurves_of`) | Trust Blender's keyframe preference in background renders (it slides instead of jumping) |
| Name new JSON fields so they don't clash with existing ones | Reuse a name like `hold` (it already means "frames to wait"; that's why props are `carry`) |
| Remember brow angles: **negative = worried/sad**, positive = angry/determined | Guess the sign |
| Make every pipeline change **opt-in from the episode JSON** | Change how the Shorts or older episodes behave |
| Keep shared character, motion and voice settings as they are unless the user agrees | Retune voices or characters per episode |
| Commit only when the user asks | Commit or push on your own |

---

## Part 1: 50 problems to fix

### Bodies and acting
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| B1 | Everyone always faces the camera; only the head turns | 3/4 body view per character (turned torso, legs, tail) | L | 1 | doing (chest details turn with the head; true 3/4 body art per character later) |
| B2 | Walking is a sidestep facing the camera | A side-view walk cycle (profile body) for walks on/off | L | 1 | later (needs side-view art per character) |
| B3 | Sitting is just shorter legs | A real sitting pose: bent knees, feet on the floor, hands on knees | M | 1 | done (sitting: knees forward, shins down, legs apart) |
| B4 | No sit-down / stand-up moves; characters pop into a seat | Transition moves: lower into the seat, push up from it | M | 2 | todo |
| B5 | Rocco "asleep" isn't possible | Sleeping pose: eyes shut, head tipped, slow breathing, little "z" | S | 1 | done ("asleep" face + sleep move + zzz; beat "asleep": [...]) |
| B6 | No lying or slouching (beanbag, floor, step) | Slouch and sprawl poses for sitters | M | 3 | todo |
| B7 | No touching between characters (pat, high five, shoulder bump, hug) | Contact moves that reach a neighbour's spot | M | 2 | todo |
| B8 | Hands don't really touch the set (the porch switch is only timing) | Reach-to-point moves: paw to a painting pixel, then the effect fires | M | 2 | todo |
| B9 | Neighbours on the sofa overlap oddly (an arm through a friend) | Depth rules for gestures between seated neighbours | S | 2 | todo |
| B10 | Listening reactions repeat the same nod pattern | More listen variations; pick by character and mood | S | 2 | todo |
| B11 | The group laugh looks the same each time | Laugh variants per character with different lengths and starts | S | 3 | todo |
| B12 | Missing faces: embarrassed, sad, scared, sleepy-talking, determined | New expressions (one table row each) plus ear/tail moods | S | 1 | done (sad, embarrassed, scared, determined, asleep) |
| B13 | Big moves have no anticipation (walks start instantly) | A small counter-move before walks, sits, jumps | S | 2 | done (dip and lean back before every walk) |
| B14 | Emotional lines use the same lip sync and gestures as jokes | "Quiet" acting: smaller mouth, no gestures, slower blinks | S | 1 | done (line "quiet": true: smaller acting, no gestures) |
| B15 | Tails and ears can poke through front pieces (railing, sofa) | Keep tails behind fronts; check per spot | S | 2 | done (tails sit behind front pieces by depth) |

### Camera and staging
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| C1 | Captions cover characters' bodies at the bottom of the frame | Move captions above or beside faces, or lift the camera framing | S | 1 | done (captions lower on painted sets) |
| C2 | The game card can cover faces or key set details | Place the card on the emptiest side of the shot | S | 2 | todo |
| C3 | Insert and close shots go soft (the 4K painting is enlarged) | 8K upscale of key areas, or a separate close-up painting | M | 2 | todo |
| C4 | Same set, new spot = a jump cut (Riot teleports from tower to sand) | Walk between spots inside a beat, or cut to another angle | M | 1 | done (beat "walk_to": walk to another spot mid-scene and stay; between sets, cut) |
| C5 | One painting per place = one camera angle; no reverse shots | A second painting per main set (the opposite view) | M | 2 | todo |
| C6 | The camera never follows someone walking | A follow pan that tracks the walker | S | 2 | todo |
| C7 | Too many wide shots in a row | A shot-variety rule per scene: wide, then medium, then close | S | 1 | done (rule in part 2) |
| C8 | Screen direction isn't tracked (left/right continuity) | Note each scene's entry and exit side and keep it consistent | S | 3 | done (rule in part 2: note entry/exit sides) |
| C9 | The group chat is a caption box, not a phone screen | A messaging graphic: bubbles pop in one by one, no app UI invented | M | 1 | done (beat "chat": bubbles pop in one by one, sender colours, pop sound; long chats scroll, 4 on screen, and the beat lasts until the last one has been read) |
| C10 | No intro sequence or episode title card | The ~10 s intro and theme, plus a title card | L | 1 | done (intro beat: night lake camera move + PORCHLIGHT title fx; a written theme tune later) |

### Sets and the world
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| W1 | Painted fireflies and lights are frozen beside our moving ones | Paint out frozen effects (ask Gemini for "no fireflies") or cover them | S | 2 | done for new sets (template forbids painted effects); Ep 1 stoop still has them |
| W2 | Painted trees and grass never move | Cut tree crowns as separate pieces and sway them | M | 2 | todo |
| W3 | Clouds and sky are frozen | Cut clouds and drift them slowly | S | 3 | todo |
| W4 | Water only has glints; the painted surface is still | A soft moving ripple overlay on water areas | S | 3 | todo |
| W5 | The ceiling fan doesn't turn | Cut the blades and spin them | S | 2 | todo |
| W6 | A lamp switching on only adds a glow; the room doesn't brighten | Lamp on and off also changes the set tint and the cast light | S | 1 | done (lamp_on also warms the whole place) |
| W7 | Painted props (snack bowls, board games) can't be used | Cut key props as pieces that can move or be picked up | M | 3 | todo |
| W8 | Lord Puddles never moves | Blink, throat puff and an occasional head turn | S | 2 | done (blinks; looks up at the light in the stoop scene) |
| W9 | The duck only bobs; the script says it "turns away" | Several duck poses switched on cue | S | 2 | done (critter "poses" on cue: the duck turns away, then looks back) |
| W10 | No weather (ep 5 needs the yearly storm) | Rain, lightning flash, wind on plants, darker grade | M | 1 | done (beat "weather": "storm": rain, double lightning flash, thunder, darker sky, rain sound) |
| W11 | New sets need spots typed in by hand (pixel guessing) | A small tool: click spots and front outlines on the painting | M | 1 | done (tools/spot_picker.html: click spots, fronts, lamps; copy JSON) |
| W12 | Every set must be repainted to match (Gemini drift between sets) | A style reference pack and a fixed prompt template per set type | S | 1 | done (art/SET_PROMPT_TEMPLATE.md) |

### Light and colour
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| L1 | Characters have no form shading from the set's light direction | Shadow side on the cast, set per painting (light from left or right) | M | 2 | todo |
| L2 | No rim light at night or at sunset | A thin bright edge on the side facing the light | M | 3 | todo |
| L3 | The set light on the cast is one flat amount | Graded light: brighter toward the source | M | 3 | todo |
| L4 | Night scenes can get too dark on small phone screens | A brightness check per still (minimum face brightness) | S | 2 | todo |
| L5 | Each set is graded on its own; cuts between sets jump in colour | A whole-episode colour pass: same warmth within a time of day | S | 2 | todo |

### Sound
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| S1 | Room tones cut hard between scenes | Short crossfades at scene changes | S | 1 | done (fixed again 29 Oct: the old fades dipped to near-silence at every cut; now the tones overlap with equal-power fades, beats in the same place share one tone, and the 8 s loops no longer click or jump) |
| S2 | Voices sound the same near or far | Distance: back spots a little quieter and softer | S | 3 | todo |
| S3 | Small actions have no sound (phone tap, cushion, chip bag) | A foley set tied to moves (munch, sit, phone) | S | 2 | doing (chip crunch on munch; phone taps and cushion sounds later) |
| S4 | Music doesn't react to emotional moments | Duck or soften the bed on quiet lines; a soft piano bed | S | 1 | done (music steps back under quiet lines) |
| S5 | Whispers and shouts use the same voice level | Per-line "whisper" and "shout" voice styles | M | 2 | todo |

### Writing for animation
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| A1 | Scripts ask for things the engine can't do (fox tail only, duck turning away) | Script rule: check the JSON features table before writing actions | S | 1 | done (rule in part 2) |
| A2 | Long dialogue scenes with no physical business | Every scene gets one piece of business (a prop, a walk, an object) | S | 1 | done (rule in part 2) |
| A3 | Jokes rely on words only | One visual gag per episode that works with the sound off | S | 2 | done (rule in part 2) |


## Part 1b: 50 more problems (found while the improved Episode 1 rendered, 29 Oct)

### Acting and character
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| D1 | Every character walks the same way | Personal walks: Riot bouncy, Bash heavy and wide, Pip quick little steps, Rocco a lazy shuffle | M | 1 | done (WALK_STYLE per character) |
| D2 | All characters are the same height | Species heights: Bash biggest, Pip smallest, Riot and Rocco between | S | 1 | done (HEIGHT: Bash 1.1, Pip 0.92 on painted sets) |
| D3 | No reaction shots: the camera stays on the speaker at the punchline | Cut to the listener's face for the reaction on key lines | S | 1 | done (line "react": "who") |
| D4 | The "stare at the camera" gag has no proper move | A camera stare: head turns to us, holds, small blink, then back | S | 1 | done (do "stare") |
| D5 | Takes (surprise) are small; no cartoon stretch | Bigger takes: eyes pop, body stretches up, snaps back | S | 2 | later |
| D6 | Idle motion repeats noticeably in long scenes | More idle variations, chosen at random per character | S | 2 | later |
| D7 | Characters may blink at the same moment | Offset blinks per character so they never sync | S | 2 | done (blinks are seeded per character) |
| D8 | Few hand shapes (point, fist, open) | More: holding a phone, counting, thumbs, a little wave, scratching the head | M | 2 | later (new hand art) |
| D9 | Pip's sweat drops aren't tied to his nervous lines | Sweat appears automatically with nervous or scared faces | S | 2 | done (sweat on nervous/scared lines) |
| D10 | Listeners rarely cross arms, lean or put hands on hips | Listening poses chosen by mood (crossed arms when sceptical) | S | 2 | later |
| D11 | Nobody moves to the music in party scenes | Light head bob to the beat during party moods | S | 3 | done (heads nod to the beat in party scenes) |
| D12 | Bash yelling has no impact | A small screen shake on his loudest lines | S | 3 | done (small shake on Bash's yelling lines) |
| D13 | Shrugs and facepalms aren't used in comedy beats | A writing rule: one body gag per scene from the moves list | S | 2 | done (rule in part 0 and 2) |

### Camera and editing
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| E1 | No depth of field: backgrounds stay sharp in close-ups | Soft blur on the painting in close shots (a blurred copy of the plate) | M | 2 | later |
| E2 | No snap zoom on punchlines | A quick push-in on the joke line, then hold | S | 1 | done (line "punch": snap zoom + soft sting) |
| E3 | Emotional lines don't get a slow push-in automatically | "quiet" lines get a slow push-in | S | 1 | done (quiet lines push in slowly) |
| E4 | Only hard cuts between scenes | Fades to black for time jumps; quick dissolves between places | S | 1 | done (beat "transition": "fade") |
| E5 | No "later that night" style time cards | A small time card fx (text over a held wide shot) | S | 2 | done (fx "card") |
| E6 | Spooky moments are framed like normal ones | A slight tilted (dutch) angle and slow creep for tense beats | S | 2 | later (camera rotation not in CamAnim yet) |
| E7 | The cold open looks like the rest of the show | Letterbox bars for cold opens: a cinematic feel | S | 3 | done (beat "letterbox") |
| E8 | No camera shake on thunder or big hits | Shake tied to thunder and slams | S | 2 | done (thunder shakes the camera) |
| E9 | The hook text in the first second is a plain black box | A styled hook card that matches the title look | S | 2 | done (Porchlight hook text styled like the title) |
| E10 | Pauses after jokes are fixed, not tuned per joke | "laugh room" per line: a little longer after big jokes | S | 2 | done (line "pause" before the next line) |

### Sets and world
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| F1 | Doors never open | Cut the door from the painting; swing it open and shut on exits | M | 1 | later (cut doors per set) |
| F2 | Window lights never change | Windows light up or go dark (time passing, someone going to bed) | S | 2 | done (lamp_on on windows) |
| F3 | The town feels empty | Tiny background townsfolk walking by in the distance | M | 2 | later (needs small townsfolk art) |
| F4 | No birds in the day sky | Small birds crossing now and then | S | 2 | done (life "birds") |
| F5 | No moths around the street lamps at night | Moths circling lamps | S | 3 | done (life "moths") |
| F6 | The lake shore has no moving water line | Gentle foam or ripples along the shoreline | S | 3 | done (life "shore": a moving foam line) |
| F7 | The hall's torn curtain hangs frozen | Cut the curtain and sway it slowly (spooky but calm) | S | 2 | later |
| F8 | Nothing reacts when someone enters the hall | A little dust falling from the beams when the door opens | S | 3 | done (hall dust drifts in the moonbeams) |
| F9 | No chimney smoke or steam (snack bowls, mugs) | Thin smoke and steam wisps | S | 3 | done (life "steam") |
| F10 | Characters cast no shadow on walls indoors | Soft wall shadows behind characters in the apartment and hall | S | 2 | later (needs per-spot wall distance) |
| F11 | Bikes and cars never pass on the street | An occasional bike rolling by at the back | S | 3 | later |
| F12 | Sets have no "props on the move" (leaves blowing, a ball rolling) | Small random life per set: a leaf drifting, a paper skittering | S | 3 | done (life "leaves") |

### Light
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| G1 | The flashlight doesn't light the characters it hits | Brighten characters inside the beam | M | 2 | later |
| G2 | Phone screens don't glow on faces at night | A soft glow on the face when a phone is up at night | S | 2 | done (phone glow on Riot's face at night) |
| G3 | Lightning doesn't light up the characters | The flash also brightens the cast for a frame | S | 2 | done (the flash brightens everything, cast included) |
| G4 | Eyes never catch the light at night | A small eye shine near lamps and in the flashlight | S | 3 | later |
| G5 | Sunset has no glow on the ears and edges | Warm edge glow on the sun side at sunset | M | 3 | later |

### Sound and music
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| H1 | No Porchlight theme melody | A short theme motif for the intro and the porch-light ending | M | 1 | done ("theme" motif: intro and under the logo) |
| H2 | Jokes have no little musical hit | Soft stings on punchlines (not on every one) | S | 2 | done (with punch lines) |
| H3 | Voices are always centred | Pan voices left or right by where the character stands | S | 2 | later (the mixer is mono; needs a stereo mix) |
| H4 | Indoors and outdoors voices sound the same (only the hall has echo) | A small room sound on all indoor voices, open air outdoors | S | 2 | done (apartment voices get a small room) |
| H5 | No breath before emotional lines | A soft breath sound before quiet lines | S | 3 | done ("breath" before quiet lines) |
| H6 | The town is silent in the distance | Far-off town sounds: a dog, a screen door, a bike bell | S | 3 | later |
| H7 | The lo-fi loop repeats every 25 seconds | Longer, varied lo-fi beds (a few versions that alternate) | M | 2 | done (lofi: 8 chords, 16 bars, ~49 s loop) |

### Episode polish
| # | Problem | Fix idea | Effort | Prio | Status |
|---|---|---|---|---|---|
| J1 | The thumbnail is picked automatically and uses the first set | Choose the thumbnail scene and pose in the episode JSON | S | 1 | done (episode "thumb": location + cast) |
| J2 | No end-of-episode beat after the logo (a quiet button) | Optional 2-second button after the logo: a sound or a tiny moment | S | 3 | later |
| J3 | The QA sheet doesn't flag animation problems | Extra checks: anyone off-frame, faces too dark, captions over faces | M | 2 | later |

---

## Part 2: per-episode checklist (copy for each episode)

### 1. Script (before writing the JSON)
- [ ] Each scene has a place that exists as a painted set, or the new set is on the build list
- [ ] Each scene has physical business: a walk, a prop, an object used (A2)
- [ ] Every action in the script is in the JSON features table (`ANIMATION_TODO.md`), or is flagged as a build item (A1)
- [ ] One visual gag works with the sound off (A3)
- [ ] Emotional lines are marked quiet (B14, S4)
- [ ] Entry and exit sides are noted for each scene (C8)

### 2. Sets (for each new place)
- [ ] Gemini prompt uses the style template, with `lake_day_v2` as the style reference (W12)
- [ ] No baked-in moving effects (fireflies, light beams) in the painting (W1)
- [ ] Day/night versions keep the same composition
- [ ] Upscaled to 4K (`tools/realesrgan`)
- [ ] Spots set: standing (4) and named sit/stand spots (W11)
- [ ] Front pieces cut (`tools/fronts.py`): furniture fronts, railings, foreground plants
- [ ] Lamps, life (fireflies, shimmer, twinkle, dust, dapple, sway), cast light, shadow and haze filled in
- [ ] Surface set for footsteps (sand, stone, wood) and room tone chosen
- [ ] Reference still of the empty set and with the cast; user OK

### 3. Episode JSON
- [ ] Spots chosen (sit on furniture where it makes sense; depth, not a line-up)
- [ ] Entrances and exits as walks, not pops (C4)
- [ ] Shot variety: wide, then medium, then close; at least one ots or at shot per long scene (C7)
- [ ] `look` used for eye-lines to objects (the light, the duck, the phone)
- [ ] Faces chosen per line; `soft` for quiet lines
- [ ] Props via `carry` and `riot_phone`; effects via `fx` (lamp_on, flashlight, critter)
- [ ] Sounds: `exit_sfx`, step sounds automatic, extra `sfx` timed

### 4. Stills review (no full render until approved)
- [ ] Pipeline stills: 2–3 frames per scene plus the ending
- [ ] Nobody off-frame or drifting; no black edges
- [ ] Nobody standing in front of furniture they should be in
- [ ] Captions and cards don't cover faces (C1, C2)
- [ ] Night faces readable (L4); colour consistent between scenes (L5)
- [ ] User OK, then render

### 5. After the render
- [ ] QA pass (length, loudness, gaps, hook)
- [ ] Watch once with sound off and once with sound only
- [ ] Note new problems at the bottom of this file for the next episode

---

## New problems found (add here after each episode)
| Episode | Problem | Idea |
|---|---|---|
| Pipeline review (29 Oct) | Parallel renders (`--jobs`): blinks, twitches, eye darts, fidgets, tail sway, birds and leaves were timed from each job's first frame, so they jumped where jobs met | Fixed: all timed from the scene's own start; a job only skips ahead |
| Pipeline review (29 Oct) | A render job starting 33+ s into a beat could show the wrong face, or crash | Fixed |
| Pipeline review (29 Oct) | `scene.blend` from a parallel render only had the first job's animation | Fixed: an extra job bakes the whole episode and saves it |
| Pipeline review (29 Oct) | Every parallel job ran Rhubarb on the same voices at once (4x the work, could corrupt the lip-sync cache) | Fixed: `make.py` makes the cues once, before rendering; files are written whole |
| Pipeline review (29 Oct) | A chat with more bubbles than the beat had time for leaked into the next scene, and 6+ bubbles ran off the bottom | Fixed (see C9) |
| Pipeline review (29 Oct) | After a `walk_to`, cameras, looks and dust still used the old spot | Fixed: shots and looks after the walk find the walker |
| Pipeline review (29 Oct) | Emotes stayed where the character was placed (a "?" hung in the air while he walked in) | Fixed: emotes ride with the character |
| Pipeline review (29 Oct) | Every copy of a character after the first (the same character in another place in the episode) lost its torso bend, walking stride, hoodie strings and chest turn: the body was found by name and Blender names copies "riot_body.001" | Fixed (`cast.body_of`) |
| Pipeline review (29 Oct) | Two new characters in one beat got the same spot | Fixed: each gets the next free spot (or a clear error) |
| Pipeline review (29 Oct) | Title letters were evenly spaced, so the narrow "I" left gaps ("PORCHL I GHT") | Fixed: spaced by each letter's width |
| Pipeline review (29 Oct) | The camera could drift back to an old shot mid-line when a reaction cut or a quiet-line push met a line's own camera | Fixed in the camera itself |
| Pipeline review (29 Oct) | Close-ups counted empty spots as bodies, so on a crowded set they backed out to a medium shot | Fixed (Ep 1's apartment close-ups get tighter on a re-render) |
| Pipeline review (29 Oct) | `--reuse-voices` after editing a line kept the old voice for good | Fixed: a later run without the flag redoes edited lines |
| Pipeline review (29 Oct) | `doctor.py` said "ALL GOOD" even if the cast code was broken | Fixed; it also checks the Blender version and the Porchlight paintings |
| Ep 2 | The haunted-house door "creaks open by itself", but doors can't open yet (F1) | Build item: cut the door from `hall_outside_*` and swing it, before Ep 2's stills |
| Ep 5 | "12 August" must be readable on Walt's calendar; paintings have no text | Use the new `label` fx on the calendar plus an `at:` insert shot |
| Ep 5, 7 | Grandpa's lantern photo must be seen; the hallway painting's photos are blank shapes (C6) | Build item: a close-up painting of the photo (`GEMINI_PROMPTS.md` C6b) for an insert shot |
