# CLAUDE.md — Porchlight

Porchlight is an animated story series starring the Friendzy cast (Riot 🦊, Rocco 🦝, Bash 🐻, Pip 🐰). It started inside the Friendzy project on 28 Oct 2026 and moved here the same day. **Read `DECISIONS.md` before doing anything**: it holds every decision the user made over 12 rounds of questions.

## Where things are
| What | Where |
|---|---|
| Decisions so far (source of truth) | `DECISIONS.md` |
| Series bible (approved) | `BIBLE.md` |
| All 40 episodes, arc by arc | `STORY_MAP.md` |
| Animation rules, known problems, per-episode checklist | `ANIMATION_CHECKLIST.md` |
| Animation fixes done + every episode JSON field | `ANIMATION_TODO.md` |
| Gemini set-painting prompts | `GEMINI_PROMPTS.md` |
| Depth layers for painted sets (tool + how-to) | `DEPTH_LAYERS.md`; tool `Blender/tools/depth_layers.py` |
| Folder overview | `README.md` |
| Rejected earlier idea (reference only) | `archive/old-series-idea/` (local folder, not in git) |
| Animation pipeline (shared with the Friendzy Shorts) | `~/Desktop/Friendzy/Blender/` — start with `doctor.py` and `README.md` there |
| Episode renderer | `python3 ~/Desktop/Friendzy/Blender/templates/make.py episode --script <ep>.json [--format horizontal]`; JSON shape in Blender `README.md` section 5; example `Blender/templates/examples/campfire-confessions/ep01.json` |
| Characters, sets, voices | `~/Desktop/Friendzy/Blender/characters/` (`CHARACTERS.md`), `Blender/voices/` |
| The Friendzy app (for real games, prompts, features) | `~/Desktop/Friendzy/` (iOS) — real prompts only, never invented app UI |

There is **one** Blender pipeline, shared with the Friendzy advertiser (which makes Shorts and must not touch Porchlight). Don't copy it here. New Porchlight sets/characters are added to the shared Blender as new additions; don't change shared character, motion, audio or voice code without asking.

## Where we are (29 Oct 2026)
1. Done: concept Q&A (rounds 1–12), `BIBLE.md` (approved, round 7), `STORY_MAP.md` arc 1 (eps 1–5, approved, round 9) and arc 2 (eps 6–10, written).
2. Done: the look. Sets are Gemini paintings in the cast's style (`lake_day_v2` is the style reference); the code-drawn cast stays; the Gemini cut-out cast experiment is closed (round 11). Episode 1 is built as episode JSON and rendered with the painted sets, seats, walks, set life, lighting, intro and porch-light ending (`ANIMATION_TODO.md`, `ANIMATION_CHECKLIST.md`).
3. Done (29 Oct): a code review of the shared Blender pipeline, tested headless on Blender 5.2; its fixes are logged at the bottom of `ANIMATION_CHECKLIST.md`.
4. **Waiting on the user:** the three arc 2 questions at the end of `STORY_MAP.md` (the smudged co-host, the festival's name, Walt's age on the storm night) and the premiere date (`DECISIONS.md` "Open").
5. Next: story map arcs 3–8 (the user reviews each arc), then full scripts in batches of 5 (`scripts/`), each turned into episode JSON. Before Ep 2–5 stills: paint the new sets (`GEMINI_PROMPTS.md` C1–C6b) and build the items flagged in the checklist's "New problems found" (the opening door for Ep 2, the photo insert for Ep 5).
6. Still to build: new characters (Mrs. Brook, Gus, Dot, Big Hal, the Mayor cat, Preston, the human hiker, Walt) with voices; a written theme tune. (Side-view walks, drawn poses, the plain-text script format and the auto-director are built: `WRITING_AN_EPISODE.md`, `ANIMATION_WINS.md`.) Premiere when 6 episodes are finished (realistically early December), then Wednesday + Saturday.

## How to do the project (the process, with the user's approval gates)
1. **Decide** with the user (numbered questions) → write it into `DECISIONS.md` immediately.
2. **Bible** (`BIBLE.md`) → user approves.
3. **Story map** (`STORY_MAP.md`, all 40 episodes) → user approves.
4. **Scripts** in batches of 5 (`scripts/epNN.md`: scene list, dialogue, on-screen text, which Friendzy game/feature appears and its real source) → user approves each batch.
5. **Episode JSON** (`episodes/epNN.json`, the renderer's format) made from each approved script.
6. **Stills first**: `make.py episode --script ... --format horizontal --stills` → show the stills sheet → user OK.
7. **Render** only approved episodes → check QA → report file paths. Never post, schedule, commit or push unless asked.
Pipeline additions (new sets, characters, moves, music) follow the same rule: build → stills/reference sheet → user OK. One thing at a time.

## Skills: how the animation pipeline works
All tools live in `~/Desktop/Friendzy/Blender/`. Its `README.md` (sections 1–9) and `characters/CHARACTERS.md` are the full manuals; read them before building. The pipeline finds this folder at `~/Desktop/Porchlight`; if it moves, set `PORCHLIGHT_DIR` (and `BLENDER` for another Blender binary). Summary:

**Setup and Blender**
- Always first: `python3 ~/Desktop/Friendzy/Blender/doctor.py` → must print `ALL GOOD` (each BAD line prints its fix).
- Blender 5.2: `/Applications/Blender.app/Contents/MacOS/Blender --background --python script.py`. One script per task; render small preview PNGs to check; save a `.blend` so the user can tweak by hand. Blender exits 0 on script errors, so check for tracebacks (make.py does).
- Don't use the Blender MCP, and don't use the HyperFrames / Remotion / brag video skills for this project.

**Making video** (run from `Blender/templates/`)
- `make.py <template> ...` = voices → timing → generated soundtrack → Blender render → mp4 + silent mp4 → QA → a row in `Blender/videos/tracker.csv`.
- Episodes: `python3 make.py episode --script <ep>.json --format horizontal --jobs 6` (6 on the M3; one more process bakes the whole episode into `scene.blend` while they render) (+ `--stills` for preview stills, `--reuse-voices` to keep generated voices, `--ones` to render every frame). Horizontal episodes render "on twos" (classic 2D look) at ~165 s of render per minute of video, so a 3–4 min episode ≈ 8–11 min.
- Episode output: mp4, `chapters.txt` (YouTube chapters), `qa.txt`, `qa_sheet.png`, `stills_sheet.png`, and a 1280×720 thumbnail (automatic for horizontal). QA: length band 120–240 s for horizontal, -14 LUFS loudness, no black gaps, no dead air > 1.2 s, hook visible early, YouTube safe zones.
- Episode JSON shape (README section 5): `series`, `episode`, `title`, `next`, optional `previously`, `thumb_text`/`thumb`, and `beats[]`. Each beat: `id`, `chapter`, `text`, `location`, `cast` ({who: costume}), `camera` (`wide`, `close:<who>`, `two:<a>,<b>`), `mood` (`normal`, `tense`, `party`), `sfx`, `lines[]` (`who`, `say`, `do`, `face`, `look`/`target`, `camera`, `pause`), optional `game` (real app moments: `nhie`, `mlt`, `td`, `alias`, `feature`), `prop`, `after[]`, `hold`.
- Thumbnails/covers: `python3 thumbnail.py ../videos/<name> [--cover] [--text "2-4 WORDS"]`.
- Several renders in one go: `render_week.py <jobs>.json [--dry-run]` (README 7d) skips finished work and keeps going after failures.
- App features on a real phone screen: the `feature` template / `"game": {"type": "feature"}` beats use real App Store screenshots only (`templates/features.py`, README 7b). Real game prompts: `python3 prompts.py <game> 10` (999+ real prompts, family-safe filter).

**Characters** (`characters/`)
- `cast.py` draws the cast in code: `riot(costume)` with costumes `hoodie`, `mafia`, `dare`, `coach`, `host`, `lifeguard` (Porchlight); plus Bash (bear), Pip (bunny), Rocco (raccoon). Shared expressions; head turns; poses; lip sync with 8 mouth shapes (Rhubarb, runs via Rosetta).
- `motion.py`: idle life, ear/tail springs, moves (take, laugh, cheer, nervous, yell, shrug, facepalm, wave, thumbs, present, hop, double_take, point, munch), `talk()` with gestures per character, `motion.ACT` scales how big the acting is, camera drift, and automatic blinks/anticipation/smears.
- `props.py`: app-style cards, phones, captions, end cards. `locations.py`: sets `campfire`, `living_room(day|night)`, `car`, `game_show`, `village_night`, `party_room`; `locations.widen()` makes the 16:9 version. `layout.py`: place things by fraction of the frame; 16:9 text uses `F.text_scale`.
- Reference sheets for everything: `characters/refs/`. New characters and sets are **added** as new functions (don't rewrite existing ones), with a reference sheet for the user to approve.

**Voices** (`Blender/voices/`, 100% generated, free)
- Each character has a Kokoro base voice (`voices/refs/<who>.wav`: riot am_puck, bash am_onyx, pip af_sky, rocco am_michael, narrator bm_george) that Chatterbox clones and acts. `voices/speak.py` holds per-character pitch/exaggeration. **Never change those settings per episode.**
- New characters (Mrs. Brook, Gus, Dot, Big Hal, Preston, the hiker, grandpa in stories) need new base voices via `voices/make_refs.py` + an entry in `speak.py`; play samples to the user before using them.
- The install needs `setuptools<81` (the watermarker imports pkg_resources).

**Sound and music** (`Blender/audio/sfxkit.py`, `templates/mix.py`)
- Every sound effect, sting and music bed is synthesized. No recorded sound libraries, no licensed music, no recorded human voices.
- Episodes get one music bed per run of same-mood beats (`normal`, `tense`, `party`); Porchlight uses the lo-fi bed for normal scenes (`"beds": {"normal": "lofi"}`) and the short Porchlight motif (`theme`) on the intro and under the logo. A full written theme tune is still to do.

**Writing rules carried over from the Shorts** (`templates/WRITING.md`)
- Laugh with, never at: nobody is mocked, the target laughs along. Riot drives scenes but isn't a stage hog. Family-safe prompts only. Grab attention in the first seconds of each episode (cold open).

## What the episode tool can and can't do (Porchlight build list)
Every Porchlight field is listed in `ANIMATION_TODO.md` ("How to use it in an episode JSON"). Built so far: beats without Riot (`riot_optional`), the painted sets (`lake`, `lake_night`, `stoop_sunset`, `stoop_night`, `apartment`, `hall`) with named seats, walking on/off and between spots, the porch-light ending, the lo-fi bed and theme motif, the intro title, storms, chats, fades and letterbox, set life and set lighting. The JSON is checked before rendering (names, moves, cameras, fx), so a typo stops with a message instead of a broken render.

Not yet:
- New characters: the roster only has the four friends; Mrs. Brook, Gus, Dot, Big Hal, the Mayor cat, Preston, the hiker and Walt need building (reference sheet first) and voices.
- Sets beyond the six painted ones (hall outside, classroom, Mrs. Brook's porch, main street, Walt's dining room and hallway, Gus's garage, the town line, the festival stage): paint them (`GEMINI_PROMPTS.md`), then set their spots.
- Doors that open and plants that move as someone passes (they need the door paintings A2/A3 and the F cut-outs), narrator-only lines, a drawn three-quarter view. (Side-view walks, sit-down/stand-up, touching, drawn poses and depth layers are built.)

## How to work with this user
- Lives in Tbilisi (UTC+4); targets EU + US audiences.
- Likes being asked: rounds of numbered questions with concrete options and a recommendation. Ask before deciding anything big; when they say "you decide", decide and say what you picked.
- Plain, short language. They often dictate, so read answers generously and confirm anything ambiguous.
- Commit, push, post or schedule only when asked.

## Keeping records
Every decision the user makes goes into `DECISIONS.md` right away (and rejected ideas into its "Rejected" list), so any session can continue.

## Hard rules
- Videos are **Blender 2D only**, driven headless with `--background` Python scripts (not the Blender MCP). Remotion/HyperFrames are rejected ("AI slop").
- **The code-drawn cast is the cast.** The Gemini art cut-out rig (`artrig.py`) was rejected for the Shorts and, after a second try, for Porchlight too (round 11: stiff, off-model). Gemini paints the sets only, in the cast's style.
- Sounds, voices and music are generated (local Chatterbox/Kokoro voices, generated SFX/music). No licensed music.
- While building pipeline pieces, prove them with **stills / reference sheets, not full renders** (renders take too long). Full renders only for approved episodes.
- Family-friendly for teens and adults: no cringe, no sarcasm, no romance; the four friends are all boys; spooky is fine, truly creepy is not.
- Friendzy appears naturally (it's just the app they use); never "download now". Episodes end with the porch light clicking off + a small Friendzy logo.
- Fans must not be able to solve the secret before the finale.
