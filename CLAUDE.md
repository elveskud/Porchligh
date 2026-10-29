# CLAUDE.md — Porchlight

Porchlight is an animated story series starring the Friendzy cast (Riot 🦊, Rocco 🦝, Bash 🐻, Pip 🐰). It started inside the Friendzy project on 28 Oct 2026 and moved here the same day. **Read `DECISIONS.md` before doing anything**: it holds every decision the user made over 5 rounds of questions.

## Where things are
| What | Where |
|---|---|
| Decisions so far (source of truth) | `DECISIONS.md` |
| Folder overview | `README.md` |
| Rejected earlier idea (reference only) | `archive/old-series-idea/` |
| Animation pipeline (shared with the Friendzy Shorts) | `~/Desktop/Friendzy/Blender/` — start with `doctor.py` and `README.md` there |
| Episode renderer | `python3 ~/Desktop/Friendzy/Blender/templates/make.py episode --script <ep>.json [--format horizontal]`; JSON shape in Blender `README.md` section 5; example `Blender/templates/examples/campfire-confessions/ep01.json` |
| Characters, sets, voices | `~/Desktop/Friendzy/Blender/characters/` (`CHARACTERS.md`), `Blender/voices/` |
| The Friendzy app (for real games, prompts, features) | `~/Desktop/Friendzy/` (iOS) — real prompts only, never invented app UI |

There is **one** Blender pipeline, shared with the Friendzy advertiser (which makes Shorts and must not touch Porchlight). Don't copy it here. New Porchlight sets/characters are added to the shared Blender as new additions; don't change shared character, motion, audio or voice code without asking.

## Where we are (28 Oct 2026)
1. Done: concept Q&A (rounds 1–5), project moved here, and a ChatGPT review that connected the plot into one story (DECISIONS.md "ChatGPT review — agreed plot changes": cause and effect of the secret, the boys' roles, the 8-arc pacing table, Mrs. Brook saved for the end).
2. **Waiting on the user** for the open answers (bottom of `DECISIONS.md`), including: where the porch light is (Riot and Rocco live in an apartment), and whether Shorts should avoid any pre-premiere build-up (Claude's reading: yes, no build-up).
3. Next: write `BIBLE.md` (world, cast with ages and secrets, new characters, rules of the secret with the full answer, tone and joke rules, Friendzy's place, easter-egg system, website extras).
4. Then `STORY_MAP.md`: all 40 episodes, one paragraph each (8 arcs of 5; twist at 20; finale at 40; about 1 in 3 episodes a break from the mystery). The user approves it.
5. Then full scripts in batches of 5 (`scripts/`), each turned into episode JSON for the renderer.
6. Blender build (1–2 weeks): Maple Hollow sets (lake, forest, street, apartment, school, haunted house / old festival hall, festival stage), new characters (Mrs. Brook, Gus, Dot, Big Hal, the Mayor cat, Preston, the human hiker), walking, more expressions, golden-hour summer look, lo-fi music, ~10 s intro. Premiere when 6 episodes are finished (realistically early December), then Wednesday + Saturday.

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
All tools live in `~/Desktop/Friendzy/Blender/`. Its `README.md` (sections 1–9) and `characters/CHARACTERS.md` are the full manuals; read them before building. Summary:

**Setup and Blender**
- Always first: `python3 ~/Desktop/Friendzy/Blender/doctor.py` → must print `ALL GOOD` (each BAD line prints its fix).
- Blender 5.2: `/Applications/Blender.app/Contents/MacOS/Blender --background --python script.py`. One script per task; render small preview PNGs to check; save a `.blend` so the user can tweak by hand. Blender exits 0 on script errors, so check for tracebacks (make.py does).
- Don't use the Blender MCP, and don't use the HyperFrames / Remotion / brag video skills for this project.

**Making video** (run from `Blender/templates/`)
- `make.py <template> ...` = voices → timing → generated soundtrack → Blender render → mp4 + silent mp4 → QA → a row in `Blender/videos/tracker.csv`.
- Episodes: `python3 make.py episode --script <ep>.json --format horizontal --jobs 4` (+ `--stills` for preview stills, `--reuse-voices` to keep generated voices, `--ones` to render every frame). Horizontal episodes render "on twos" (classic 2D look) at ~165 s of render per minute of video, so a 3–4 min episode ≈ 8–11 min.
- Episode output: mp4, `chapters.txt` (YouTube chapters), `qa.txt`, `qa_sheet.png`, `stills_sheet.png`, and a 1280×720 thumbnail (automatic for horizontal). QA: length band 120–240 s for horizontal, -14 LUFS loudness, no black gaps, no dead air > 1.2 s, hook visible early, YouTube safe zones.
- Episode JSON shape (README section 5): `series`, `episode`, `title`, `next`, optional `previously`, `thumb_text`/`thumb`, and `beats[]`. Each beat: `id`, `chapter`, `text`, `location`, `cast` ({who: costume}), `camera` (`wide`, `close:<who>`, `two:<a>,<b>`), `mood` (`normal`, `tense`, `party`), `sfx`, `lines[]` (`who`, `say`, `do`, `face`, `look`/`target`, `camera`, `pause`), optional `game` (real app moments: `nhie`, `mlt`, `td`, `alias`, `feature`), `prop`, `after[]`, `hold`.
- Thumbnails/covers: `python3 thumbnail.py ../videos/<name> [--cover] [--text "2-4 WORDS"]`.
- Several renders in one go: `render_week.py <jobs>.json [--dry-run]` (README 7d) skips finished work and keeps going after failures.
- App features on a real phone screen: the `feature` template / `"game": {"type": "feature"}` beats use real App Store screenshots only (`templates/features.py`, README 7b). Real game prompts: `python3 prompts.py <game> 10` (999+ real prompts, family-safe filter).

**Characters** (`characters/`)
- `cast.py` draws the cast in code: `riot(costume)` with costumes `hoodie`, `mafia`, `dare`, `coach`, `host`; plus Bash (bear), Pip (bunny), Rocco (raccoon). Shared expressions; head turns; poses; lip sync with 8 mouth shapes (Rhubarb, runs via Rosetta).
- `motion.py`: idle life, ear/tail springs, moves (take, laugh, cheer, nervous, yell, shrug, facepalm, wave, thumbs, present, hop, double_take, point, munch), `talk()` with gestures per character, `motion.ACT` scales how big the acting is, camera drift, and automatic blinks/anticipation/smears.
- `props.py`: app-style cards, phones, captions, end cards. `locations.py`: sets `campfire`, `living_room(day|night)`, `car`, `game_show`, `village_night`, `party_room`; `locations.widen()` makes the 16:9 version. `layout.py`: place things by fraction of the frame; 16:9 text uses `F.text_scale`.
- Reference sheets for everything: `characters/refs/`. New characters and sets are **added** as new functions (don't rewrite existing ones), with a reference sheet for the user to approve.

**Voices** (`Blender/voices/`, 100% generated, free)
- Each character has a Kokoro base voice (`voices/refs/<who>.wav`: riot am_puck, bash am_onyx, pip af_sky, rocco am_michael, narrator bm_george) that Chatterbox clones and acts. `voices/speak.py` holds per-character pitch/exaggeration. **Never change those settings per episode.**
- New characters (Mrs. Brook, Gus, Dot, Big Hal, Preston, the hiker, grandpa in stories) need new base voices via `voices/make_refs.py` + an entry in `speak.py`; play samples to the user before using them.
- The install needs `setuptools<81` (the watermarker imports pkg_resources).

**Sound and music** (`Blender/audio/sfxkit.py`, `templates/mix.py`)
- Every sound effect, sting and music bed is synthesized. No recorded sound libraries, no licensed music, no recorded human voices.
- Episodes get one music bed per run of same-mood beats (`normal`, `tense`, `party`). The lo-fi theme and intro music still need building as generated music.

**Writing rules carried over from the Shorts** (`templates/WRITING.md`)
- Laugh with, never at: nobody is mocked, the target laughs along. Riot drives scenes but isn't a stage hog. Family-safe prompts only. Grab attention in the first seconds of each episode (cold open).

## What the episode tool can't do yet (Porchlight build list)
- Every beat must contain Riot (`episode_script.py` stops otherwise); scenes without Riot need this rule relaxed.
- Only the 7 Friendzy sets exist; Maple Hollow sets (lake, forest, street, apartment, school, haunted house / old festival hall, festival stage, Mrs. Brook's porch, Gus's garage, the town line) must be built.
- No walking between places, no new characters, no narrator-only beats on screen, no intro sequence, no "porch light clicks off + small Friendzy logo" ending (the current end card says "Next episode: ..."), no lo-fi music bed, no golden-hour summer lighting.
- The Gemini cut-out experiment: Riot only so far (`artrig.py`); Bash, Pip and Rocco would need Gemini art packs (prompts in `GEMINI_PROMPTS.md`) for a fair comparison.

## How to work with this user
- Lives in Tbilisi (UTC+4); targets EU + US audiences.
- Likes being asked: rounds of numbered questions with concrete options and a recommendation. Ask before deciding anything big; when they say "you decide", decide and say what you picked.
- Plain, short language. They often dictate, so read answers generously and confirm anything ambiguous.
- Commit, push, post or schedule only when asked.

## Keeping records
Every decision the user makes goes into `DECISIONS.md` right away (and rejected ideas into its "Rejected" list), so any session can continue.

## Hard rules
- Videos are **Blender 2D only**, driven headless with `--background` Python scripts (not the Blender MCP). Remotion/HyperFrames are rejected ("AI slop").
- **Gemini art cut-out rig = experiment only.** It was rejected for the Shorts ("parts just floating around"), but the user wants to try it again for Porchlight (`Blender/characters/art/`, `artrig.py`, `GEMINI_PROMPTS.md`). Compare it with the code-drawn cast on stills; the code-drawn cast stays the default until the user picks. Never switch the Shorts to it.
- Sounds, voices and music are generated (local Chatterbox/Kokoro voices, generated SFX/music). No licensed music.
- While building pipeline pieces, prove them with **stills / reference sheets, not full renders** (renders take too long). Full renders only for approved episodes.
- Family-friendly for teens and adults: no cringe, no sarcasm, no romance; the four friends are all boys; spooky is fine, truly creepy is not.
- Friendzy appears naturally (it's just the app they use); never "download now". Episodes end with the porch light clicking off + a small Friendzy logo.
- Fans must not be able to solve the secret before the finale.
