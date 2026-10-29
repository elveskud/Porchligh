# 200 small wins for animation quality

The user asked (29 Oct 2026) for up to 200 small improvements toward the goal: **write a short script, get a
high-end episode, spend few tokens per episode.** Each is checked with small stills, never a full render.
Status: `todo`, `done`, `art` (needs a painting or drawing from the user / Gemini first), `no` (decided against, with why).
Effort: S = under an hour, M = a few hours, L = a day or more. Items already done before this list are in
`ANIMATION_TODO.md` and `ANIMATION_CHECKLIST.md` and aren't repeated.

## A. The script (writing an episode cheaply)
| # | Win | Effort | Status |
|---|---|---|---|
| 1 | Plain-text screenplay format that `make.py` turns into episode JSON | M | done |
| 2 | Scene headings: `== lake, day \| riot (lifeguard), rocco` | S | done |
| 3 | Faces in brackets: `RIOT (nervous): ...` | S | done |
| 4 | Entrances: `BASH enters left` | S | done |
| 5 | Exits: `ROCCO exits right` | S | done |
| 6 | Moving: `RIOT walks to the step` | S | done |
| 7 | `(whispers)` / `(quietly)` makes a quiet line | S | done |
| 8 | `[sfx: door]` sound cues | S | done |
| 9 | `[card: Later that night.]` time cards | S | done |
| 10 | `[chat]` blocks: `Riot: LIGHT'S ON` | S | done |
| 11 | `[game nhie: prompt \| target \| confession]` game moments | M | done |
| 12 | Porchlight defaults on: auto-director, porch-light ending, lo-fi bed, Riot optional | S | done |
| 13 | Sitters sit: on a set with seats, characters take them unless told to stand | S | done |
| 14 | Chapters from scene headings | S | done |
| 15 | The hook text defaults to the first line when none is given | S | done |
| 16 | Time of day picks the set: `lake, night` → `lake_night` | S | done |
| 17 | Script lint: very long lines, scenes with nobody doing anything | S | done |
| 18 | Length estimate before voicing (is it inside 2–4 minutes?) | S | done |
| 19 | The generated JSON is written next to the script, so it can be read | S | done |
| 20 | Unknown names give a clear error listing who exists | S | done |

## B. The auto-director (shots and editing)
| # | Win | Effort | Status |
|---|---|---|---|
| 21 | A new place always opens on its wide shot | S | done (a beat opens on its own wide unless the script frames it) |
| 22 | No jump cuts: never cut to the same size of shot on the same person | S | done |
| 23 | Cut on action: a cut lands just as a big move starts | S | done |
| 24 | Reaction close-up when a listener does a take or gasps | S | done (cut on the action, and reaction close-ups) |
| 25 | A scene's last quiet line gets a slow push-in (the emotional button) | S | done (quiet lines already push in) |
| 26 | Exits play on the wide shot, so the walk-off reads | S | done |
| 27 | Two-person scenes favour two-shots over the full wide | S | done |
| 28 | Group wides lean a little toward whoever is talking | S | done |
| 29 | A question holds on the asker until the answer starts | S | done (the next line's cut lands as the answer starts) |
| 30 | Nothing holds longer than ~8 s without a slow move | S | done |
| 31 | No cuts in a beat's first 12 frames | S | done (no cut within 1.2 s of a beat's start) |
| 32 | A cold open (first beat) gets letterbox bars automatically | S | done |
| 33 | Shouted lines get a quick snap-in | S | done |
| 34 | `shots.txt` lists each shot's length and flags anything under 1 s | S | done |
| 35 | Inserts (`at:` shots) creep in slowly | S | done |
| 36 | A jump in time of day between scenes fades through black | S | done |
| 37 | Dutch (tilted) angle for tense scenes | M | done |
| 38 | Follow pan on someone walking across the set | M | done |
| 39 | Game cards sit on the emptiest side of the frame | M | done |
| 40 | Close-ups never zoom past the painting's real resolution (no soft shots) | S | done (close-ups get a soft background on purpose: 161) |

## C. Acting and faces
| # | Win | Effort | Status |
|---|---|---|---|
| 41 | Questions end with a brow lift and a small head tilt | S | done |
| 42 | Nod on "yes / yeah / okay / sure" | S | done |
| 43 | Head shake on "no / nope / nah" | S | done |
| 44 | Shrug on "I don't know / dunno / whatever" | S | done |
| 45 | Wave on "hi / hey / bye / see ya" | S | done |
| 46 | Point at the listener on a forceful "you" | S | done |
| 47 | Facepalm on "seriously / ugh / oh no" | S | done |
| 48 | A sigh (breath + slump) before a line that starts with "..." | S | done |
| 49 | Listeners smile at a punchline | S | done |
| 50 | Listeners' eyes widen at a shout | S | done |
| 51 | A small chuckle from listeners after a joke | S | done |
| 52 | Ears perk when someone says your name | S | done |
| 53 | Tail wags faster on energetic lines | S | done |
| 54 | Speakers glance away mid long line, then back (thinking) | S | done |
| 55 | Eye darts in the pause before a line (deciding what to say) | S | done |
| 56 | Mouth shapes lead the sound by a frame (reads as better sync) | S | done (with `act`) |
| 57 | Closed-mouth sounds (m, b, p) always show a closed mouth | S | done (with `act`) |
| 58 | Bash breathes harder after he yells | S | done |
| 59 | Rocco's resting face is half-lidded (his deadpan) | S | done |
| 60 | Riot taps a foot while waiting | S | done |
| 61 | Bash cracks his knuckles while waiting | S | done |
| 62 | Pip fiddles with his hoodie strings while waiting | S | done |
| 63 | Listening poses by mood: crossed arms when sceptical | M | done |
| 64 | Hands on hips (Riot proud, Bash defiant) | S | done (move `hips`) |
| 65 | Laugh variants per character with different lengths | S | done |
| 66 | Bigger takes: stretch up, eyes pop, snap back | S | done |
| 67 | More idle variations, picked at random per character | M | done |
| 68 | Asleep characters stir once in a long scene | S | done |
| 69 | Characters blink when a cut lands on them | S | done |
| 70 | Pupils follow a walking character | S | done |

## D. Bodies and movement
| # | Win | Effort | Status |
|---|---|---|---|
| 71 | 3/4 body turn (torso, legs and tail turn, not just the head) | L | todo |
| 72 | Side-view walk cycle | L | todo |
| 73 | Sit-down move (lower into the seat) | M | todo |
| 74 | Stand-up move (push up from the seat) | M | todo |
| 75 | Slouch pose for sitters | M | todo |
| 76 | Lying back on the beanbag | M | todo |
| 77 | Walk: a little squash on each footfall | S | todo |
| 78 | Walk: settle with a small overshoot when stopping | S | todo |
| 79 | Run (faster steps, lean forward) for hurried entrances | M | todo |
| 80 | Sneak walk (tiptoe, crouched) for night scenes | M | todo |
| 81 | Turn toward the direction of travel before walking off | S | todo |
| 82 | Jump up from a seat on a shock | S | todo |
| 83 | Crouch / kneel to look at something on the floor | M | todo |
| 84 | Arms crossed as a move (`do: cross`) | S | done (move `cross`) |
| 85 | Hands in the hoodie pocket (idle) | S | todo |
| 86 | Lean on a railing or wall | M | todo |
| 87 | Stretch (arms up) move | S | done (move `stretch`) |
| 88 | Yawn move | S | done (move `yawn`) |
| 89 | Scratch the head (confused) move | S | done (move `scratch`) |
| 90 | Count on fingers, available from the JSON | S | done (move `count`) |
| 91 | Clap, available from the JSON | S | done (move `clap`) |
| 92 | Peace / horns / thumbs signs, available from the JSON | S | done (moves `peace`, `horns`, `thumbs`) |
| 93 | Rock-on head-bang, available from the JSON | S | done (move `rock`) |
| 94 | Gloom (rain cloud) defeat, available from the JSON | S | done (move `gloom`) |
| 95 | Hop of joy on a small win | S | done (move `hop`, already built) |

## E. Interaction and physics
| # | Win | Effort | Status |
|---|---|---|---|
| 96 | Reach a paw to a point on the set (switch, door, table) | M | todo |
| 97 | High five between neighbours | M | todo |
| 98 | Shoulder bump | M | todo |
| 99 | Friendly hug (family-safe) | M | todo |
| 100 | Hand on a friend's shoulder (comfort) | M | todo |
| 101 | Pick a prop up: it appears in the paw on contact | M | todo |
| 102 | Put a prop down | M | todo |
| 103 | Throw a prop: an arc, a spin, a bounce | M | todo |
| 104 | Drop a prop: fall, bounce twice, settle | M | todo |
| 105 | Doors that open and shut | M | art |
| 106 | A paw flicks the light switch when the light comes on | S | todo |
| 107 | Phone taps: the thumb taps, the screen glows | S | todo |
| 108 | Sip from the cup | S | todo |
| 109 | Crumbs fall when Rocco munches | S | todo |
| 110 | The cushion squashes when someone flops onto it | S | todo |
| 111 | A splash when something hits the lake | S | todo |
| 112 | Little sand puffs on each footstep on the beach | S | todo |
| 113 | Storm wind pushes ears and tails | S | todo |
| 114 | Rain darkens the cast a little (wet) | S | todo |
| 115 | Fur stands on end on a big scare | S | todo |
| 116 | Props wobble on thunder | S | todo |
| 117 | Walkers pass in front of or behind people, never through them | S | todo |
| 118 | A character's shadow lengthens as they walk away | S | todo |
| 119 | Seated characters bounce a little when a neighbour sits | S | todo |
| 120 | Carried props swing a little on a walk | S | todo |

## F. Sets and the world
| # | Win | Effort | Status |
|---|---|---|---|
| 121 | Drifting clouds over day skies | M | todo |
| 122 | A soft moving ripple layer on water | M | todo |
| 123 | Tiny townsfolk silhouettes walking far away | M | todo |
| 124 | A bike rolls by in the distance now and then | S | todo |
| 125 | Stars twinkle on night skies | S | todo |
| 126 | The moon has a soft breathing glow | S | todo |
| 127 | Far-off porch lights twinkle in town at night | S | todo |
| 128 | Dragonflies over the lake by day | S | todo |
| 129 | A fish jumps now and then (ripple rings) | S | todo |
| 130 | Pollen / dandelion seeds drifting on summer days | S | todo |
| 131 | Low fog drifting in the hall at night | S | todo |
| 132 | TV-style flicker on the apartment wall at night | S | todo |
| 133 | Heat shimmer over the sand at noon | M | todo |
| 134 | Puddles after the storm catch the light | M | todo |
| 135 | Tree sway | M | art |
| 136 | Ceiling fan turning | S | art |
| 137 | Curtain sway in the hall | S | art |
| 138 | Wall shadows behind characters indoors | M | todo |
| 139 | A lamp switched on stays on for the rest of the scene in that place | S | todo |
| 140 | The sky colour drifts through a long sunset scene | S | todo |

## G. Light and colour
| # | Win | Effort | Status |
|---|---|---|---|
| 141 | Shadow side on the cast from the set's light direction | M | todo |
| 142 | Rim light at night and sunset | M | todo |
| 143 | Flashlight beam lights the characters it touches | M | todo |
| 144 | Eye shine near lamps and in the flashlight | S | todo |
| 145 | Phone glow on any character holding a phone at night | S | todo |
| 146 | Warm bounce light from below at sunset | S | todo |
| 147 | Soft vignette on close-ups | S | todo |
| 148 | Soft bloom around lamps | S | todo |
| 149 | Night brightness floor (faces stay readable on phones) | S | todo |
| 150 | One colour pass for the whole episode (scenes in the same light match) | M | todo |
| 151 | Quiet, sad beats a touch less saturated | S | todo |
| 152 | Tense beats a touch cooler | S | todo |
| 153 | Silhouette option against a sunset | S | todo |
| 154 | Lightning flash shows the cast's silhouettes for a frame | S | todo |
| 155 | Lamp light pools on the floor flicker very slightly | S | todo |
| 156 | Characters further from a lamp get less of its warmth (graded light) | M | todo |
| 157 | Flashlight spot is brighter at its centre | S | todo |
| 158 | Close-ups get a slight extra light on the face | S | todo |
| 159 | Night scenes: moonlight edge on the side facing the moon | M | todo |
| 160 | Contact shadows under props set down | S | todo |

## H. Camera
| # | Win | Effort | Status |
|---|---|---|---|
| 161 | Depth of field: the background softens in close-ups | M | done |
| 162 | Rack focus between two characters | M | todo |
| 163 | Whip-pan transition between places | S | todo |
| 164 | Match cut on action between scenes | M | todo |
| 165 | 2.5D parallax: front pieces move faster than the painting | S | todo |
| 166 | A slight camera lag behind fast moves (handheld feel) | S | todo |
| 167 | Camera settles with a tiny overshoot after pushes | S | todo |
| 168 | Shake scaled to what caused it (thunder > slam > take) | S | todo |
| 169 | Wide shots frame by the rule of thirds | S | todo |
| 170 | Over-the-shoulder shots keep a sliver of the listener in frame | S | todo |

## I. Sound and music
| # | Win | Effort | Status |
|---|---|---|---|
| 171 | Stereo: voices panned to where the character stands | M | todo |
| 172 | Further back = a little quieter and softer | S | todo |
| 173 | Whisper voice style (breathier, quieter) | M | todo |
| 174 | Shout voice style (brighter, a touch of drive) | M | todo |
| 175 | Foley: phone taps | S | todo |
| 176 | Foley: cushion when sitting | S | todo |
| 177 | Foley: cup sip, chip bag rustle | S | todo |
| 178 | Distant town sounds (a dog, a screen door, a bike bell) | S | todo |
| 179 | Door creak tied to the door | S | art |
| 180 | Punchline stings vary, never the same twice in a row | S | todo |
| 181 | Music follows the scene's key change into tense moments | M | todo |
| 182 | Outdoor street voices get a short slap echo | S | todo |
| 183 | Footsteps land on the actual foot contact | S | todo |
| 184 | A written Porchlight theme tune (full, not just the motif) | L | todo |
| 185 | A soft piano bed option for emotional scenes | M | todo |

## J. Text, graphics and QA
| # | Win | Effort | Status |
|---|---|---|---|
| 186 | Captions move to wherever no face is | M | todo |
| 187 | Caption words pop from their centre, not their left edge | S | todo |
| 188 | Typing dots before each chat bubble | S | todo |
| 189 | Episode number + title card after the intro | S | todo |
| 190 | Emote pop has a little bounce and a soft sound | S | todo |
| 191 | "Previously" styled like the title, not a plain box | S | todo |
| 192 | QA check: anyone off-frame or cut by the frame edge mid-line | M | todo |
| 193 | QA check: faces too dark | M | todo |
| 194 | QA check: captions or cards over a face | M | todo |
| 195 | QA check: a line with nobody's mouth moving | S | todo |
| 196 | QA check: shots shorter than 1 s | S | todo |
| 197 | Stills sheet picks one frame per shot automatically (`--stills auto`) | S | todo |
| 198 | Thumbnail picks the best reaction frame automatically | M | todo |
| 199 | A reference sheet of every move and face, regenerated in one command | S | todo |
| 200 | `make.py --check`: script, JSON and shot list checks without voicing or rendering | S | done |
