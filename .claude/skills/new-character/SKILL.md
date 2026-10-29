---
name: new-character
description: Build a new Porchlight character (Mrs. Brook, Gus, Dot, Big Hal, the Mayor cat, Preston, the hiker, Walt...) in code with side view, poses and voice, behind the user's approval. Use when a script needs someone who isn't riot, bash, pip or rocco.
---
# Adding a character

The cast is code-drawn (Gemini only gives angle/pose guides; its cut-out cast was rejected twice). Add, never rewrite existing builders.

1. Ask the user for the look (species, colours, clothes, age, personality) in numbered questions; record in `DECISIONS.md`.
2. Optional guides: render them like `characters/gemini_refs.py` and give the user `GEMINI_PROMPTS.md` E1-E4 (turnaround, walk, poses, paws) with the new character's picture as image 1.
3. Front view: a new builder in `Blender/characters/cast.py`, following `bear()`/`bunny()` (`friend_body`, `add_eye`, `add_brow`, `add_mouths`, `cel(c)`), then a `roster.PROFILES` entry (`build`, `height`, `weight`, `walk=(stride, bob, step frames, arm swing, sway)`, `voice`).
4. Side view: a builder in `characters/profile.py` (`_friend()` + head shapes; facing +x) and its `STYLE` walk entry.
5. Reference sheets, run headless (`Blender --background --python <script>`): `refsheet.py` (`ONLY=<name>`), `sideref.py`, `poseref.py`. Show the user; nothing goes in an episode before their OK.
6. Voice: a Kokoro base voice via `voices/make_refs.py` + an entry in `voices/speak.py`; play samples to the user first. Never change existing characters' voice settings.
