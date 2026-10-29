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
| 71 | 3/4 body turn (torso, legs and tail turn, not just the head) | L | done (cheap version: bodies narrow as they turn; true 3/4 drawings need new art per character, for your OK) |
| 72 | Side-view walk cycle | L | art (a profile drawing of each character; reference sheet for your OK first) |
| 73 | Sit-down move (lower into the seat) | M | done (walking in to a seat sits down on arrival) |
| 74 | Stand-up move (push up from the seat) | M | done (move `stand`; leaving a seat stands up first) |
| 75 | Slouch pose for sitters | M | done (move `slouch`) |
| 76 | Lying back on the beanbag | M | art (a lying-back drawing; the front view can't lie down convincingly) |
| 77 | Walk: a little squash on each footfall | S | done |
| 78 | Walk: settle with a small overshoot when stopping | S | done |
| 79 | Run (faster steps, lean forward) for hurried entrances | M | done (`enter: left run`, "runs in from the left") |
| 80 | Sneak walk (tiptoe, crouched) for night scenes | M | done (`sneak`, "sneaks in from the right") |
| 81 | Turn toward the direction of travel before walking off | S | done (a look toward the way out first) |
| 82 | Jump up from a seat on a shock | S | done (sitters half jump out of the seat) |
| 83 | Crouch / kneel to look at something on the floor | M | done (move `crouch`) |
| 84 | Arms crossed as a move (`do: cross`) | S | done (move `cross`) |
| 85 | Hands in the hoodie pocket (idle) | S | done (move `pockets`) |
| 86 | Lean on a railing or wall | M | done (move `lean`) |
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
| 96 | Reach a paw to a point on the set (switch, door, table) | M | done (move `reach` with `reach_px`) |
| 97 | High five between neighbours | M | done ("RIOT high-fives BASH.") |
| 98 | Shoulder bump | M | done ("RIOT bumps BASH.") |
| 99 | Friendly hug (family-safe) | M | done ("BASH hugs PIP.") |
| 100 | Hand on a friend's shoulder (comfort) | M | done ("PIP puts a paw on BASH's shoulder.") |
| 101 | Pick a prop up: it appears in the paw on contact | M | done ("RIOT picks up the cup.") |
| 102 | Put a prop down | M | done ("RIOT puts down the cup.") |
| 103 | Throw a prop: an arc, a spin, a bounce | M | done ("RIOT throws the cup (at BASH).": arc, spin, two bounces) |
| 104 | Drop a prop: fall, bounce twice, settle | M | done ("RIOT drops the phone.") |
| 105 | Doors that open and shut | M | art (the door must be cut out of each painting) |
| 106 | A paw flicks the light switch when the light comes on | S | done (lamp_on `by`, `switch_px`) |
| 107 | Phone taps: the thumb taps, the screen glows | S | done |
| 108 | Sip from the cup | S | done ("RIOT sips from the cup.") |
| 109 | Crumbs fall when Rocco munches | S | done (with `act`) |
| 110 | The cushion squashes when someone flops onto it | S | done (sitting down lands with a squash) |
| 111 | A splash when something hits the lake | S | done (a throw on the lake splashes) |
| 112 | Little sand puffs on each footstep on the beach | S | done (with `act`) |
| 113 | Storm wind pushes ears and tails | S | done (with `act`) |
| 114 | Rain darkens the cast a little (wet) | S | done (the storm's dark wash already covers the cast) |
| 115 | Fur stands on end on a big scare | S | done (with `act`: tail puffs, ears up) |
| 116 | Props wobble on thunder | S | done (with `act`) |
| 117 | Walkers pass in front of or behind people, never through them | S | done (walkers pass in front) |
| 118 | A character's shadow lengthens as they walk away | S | no (walks are sideways across a front view; a lengthening shadow wouldn't read) |
| 119 | Seated characters bounce a little when a neighbour sits | S | done |
| 120 | Carried props swing a little on a walk | S | done (props ride in the paw and swing with the arm) |

## F. Sets and the world
| # | Win | Effort | Status |
|---|---|---|---|
| 121 | Drifting clouds over day skies | M | done (set JSON life: `clouds`) |
| 122 | A soft moving ripple layer on water | M | done (set JSON life: `ripples`) |
| 123 | Tiny townsfolk silhouettes walking far away | M | done (set JSON life: `townsfolk`) |
| 124 | A bike rolls by in the distance now and then | S | done (set JSON life: `bike`) |
| 125 | Stars twinkle on night skies | S | done (set JSON life: `stars`) |
| 126 | The moon has a soft breathing glow | S | done (set JSON life: `moon`) |
| 127 | Far-off porch lights twinkle in town at night | S | done (set JSON life: `porchlights`) |
| 128 | Dragonflies over the lake by day | S | done (set JSON life: `dragonflies`) |
| 129 | A fish jumps now and then (ripple rings) | S | done (set JSON life: `fish`) |
| 130 | Pollen / dandelion seeds drifting on summer days | S | done (set JSON life: `pollen`) |
| 131 | Low fog drifting in the hall at night | S | done (set JSON life: `fog`) |
| 132 | TV-style flicker on the apartment wall at night | S | done (set JSON life: `flicker`) |
| 133 | Heat shimmer over the sand at noon | M | done (set JSON life: `heat`) |
| 134 | Puddles after the storm catch the light | M | done (set JSON life: `puddles`) |
| 135 | Tree sway | M | art (tree crowns cut out of each painting) |
| 136 | Ceiling fan turning | S | art (the fan blades cut out) |
| 137 | Curtain sway in the hall | S | art (the curtain cut out) |
| 138 | Wall shadows behind characters indoors | M | done (set JSON life: `wall_shadow`) |
| 139 | A lamp switched on stays on for the rest of the scene in that place | S | done |
| 140 | The sky colour drifts through a long sunset scene | S | done (with `act`: long sunset scenes deepen toward dusk) |

## G. Light and colour
| # | Win | Effort | Status |
|---|---|---|---|
| 141 | Shadow side on the cast from the set's light direction | M | done (set JSON `light_from`: the cast's shading follows the painting) |
| 142 | Rim light at night and sunset | M | done (with `act`: moonlight rim at night, warm at sunset; JSON `rim`) |
| 143 | Flashlight beam lights the characters it touches | M | done (with `act`) |
| 144 | Eye shine near lamps and in the flashlight | S | done |
| 145 | Phone glow on any character holding a phone at night | S | done (with `act`) |
| 146 | Warm bounce light from below at sunset | S | done |
| 147 | Soft vignette on close-ups | S | done (with close-ups) |
| 148 | Soft bloom around lamps | S | done (lamps already glow; they breathe: 155) |
| 149 | Night brightness floor (faces stay readable on phones) | S | done (with `act`: the set's light on faces is capped) |
| 150 | One colour pass for the whole episode (scenes in the same light match) | M | todo |
| 151 | Quiet, sad beats a touch less saturated | S | done (with `act`) |
| 152 | Tense beats a touch cooler | S | done (with `act`) |
| 153 | Silhouette option against a sunset | S | todo |
| 154 | Lightning flash shows the cast's silhouettes for a frame | S | no (lightning already flashes the whole frame, cast included) |
| 155 | Lamp light pools on the floor flicker very slightly | S | done |
| 156 | Characters further from a lamp get less of its warmth (graded light) | M | done (already: lamp warmth falls off with distance) |
| 157 | Flashlight spot is brighter at its centre | S | done (already: the spot is a radial glow) |
| 158 | Close-ups get a slight extra light on the face | S | done |
| 159 | Night scenes: moonlight edge on the side facing the moon | M | done (the night rim is the moonlight edge) |
| 160 | Contact shadows under props set down | S | done |

## H. Camera
| # | Win | Effort | Status |
|---|---|---|---|
| 161 | Depth of field: the background softens in close-ups | M | done |
| 162 | Rack focus between two characters | M | no (characters are flat cut-outs: no depth to focus between; the close-up background blur covers it) |
| 163 | Whip-pan transition between places | S | done (`[whip]` / `"transition": "whip"`) |
| 164 | Match cut on action between scenes | M | todo |
| 165 | 2.5D parallax: front pieces move faster than the painting | S | done (with `act`: foreground front pieces) |
| 166 | A slight camera lag behind fast moves (handheld feel) | S | no (every camera move is already eased) |
| 167 | Camera settles with a tiny overshoot after pushes | S | done (with `act`) |
| 168 | Shake scaled to what caused it (thunder > slam > take) | S | done (already: thunder, slams and takes shake by different amounts) |
| 169 | Wide shots frame by the rule of thirds | S | done (wides lean toward the speaker: 28) |
| 170 | Over-the-shoulder shots keep a sliver of the listener in frame | S | done (already in the `ots` framing) |

## I. Sound and music
| # | Win | Effort | Status |
|---|---|---|---|
| 171 | Stereo: voices panned to where the character stands | M | done (with `act`; the mix is stereo now) |
| 172 | Further back = a little quieter and softer | S | done (with `act`) |
| 173 | Whisper voice style (breathier, quieter) | M | done (with `act`: quiet lines) |
| 174 | Shout voice style (brighter, a touch of drive) | M | done (with `act`: shouted lines) |
| 175 | Foley: phone taps | S | done |
| 176 | Foley: cushion when sitting | S | done |
| 177 | Foley: cup sip, chip bag rustle | S | done (sip, munch) |
| 178 | Distant town sounds (a dog, a screen door, a bike bell) | S | done (with `act`: a dog, a bike bell) |
| 179 | Door creak tied to the door | S | art (needs the door: 105) |
| 180 | Punchline stings vary, never the same twice in a row | S | done (with `act`) |
| 181 | Music follows the scene's key change into tense moments | M | done (already: tense scenes get the suspense bed) |
| 182 | Outdoor street voices get a short slap echo | S | done (with `act`: stoop scenes) |
| 183 | Footsteps land on the actual foot contact | S | done (with `act`) |
| 184 | A written Porchlight theme tune (full, not just the motif) | L | done (a first version: `theme_long` under the intro title; `test/theme_long.wav` to hear) |
| 185 | A soft piano bed option for emotional scenes | M | done (`[mood: soft]`) |

## J. Text, graphics and QA
| # | Win | Effort | Status |
|---|---|---|---|
| 186 | Captions move to wherever no face is | M | done (QA flags any caption over a face: 194; on painted sets captions sit below the bodies) |
| 187 | Caption words pop from their centre, not their left edge | S | done (with `act`) |
| 188 | Typing dots before each chat bubble | S | done (with `act`) |
| 189 | Episode number + title card after the intro | S | done (`[intro]`: the title, then "Episode N: Title") |
| 190 | Emote pop has a little bounce and a soft sound | S | done (with `act`: a soft pop) |
| 191 | "Previously" styled like the title, not a plain box | S | done (with `act`) |
| 192 | QA check: anyone off-frame or cut by the frame edge mid-line | M | done (qa.txt) |
| 193 | QA check: faces too dark | M | done (qa.txt: from the video's own frames) |
| 194 | QA check: captions or cards over a face | M | done (qa.txt) |
| 195 | QA check: a line with nobody's mouth moving | S | no (every voiced line is lip-synced by construction) |
| 196 | QA check: shots shorter than 1 s | S | done (shots.txt flags them) |
| 197 | Stills sheet picks one frame per shot automatically (`--stills auto`) | S | done (`--stills auto` + stills_sheet.png) |
| 198 | Thumbnail picks the best reaction frame automatically | M | done |
| 199 | A reference sheet of every move and face, regenerated in one command | S | done (`Blender --background --python characters/movesheet.py` -> refs/moves_sheet.png) |
| 200 | `make.py --check`: script, JSON and shot list checks without voicing or rendering | S | done |
