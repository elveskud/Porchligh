---
name: write-episode
description: Write or edit a Porchlight episode script in the plain-text format and check it cheaply. Use when the user asks for an episode, a scene, a script batch, or changes to dialogue, staging or shots.
---
# Writing a Porchlight episode

1. Read `DECISIONS.md` (rules), the episode's entry in `STORY_MAP.md`, and `WRITING_AN_EPISODE.md` (the whole format, every action and cue). Don't read pipeline code to write a script.
2. Write `episodes/epNN.txt` (on the user's Mac: `~/Desktop/Porchlight/episodes/`). Keep it short: the engine directs, acts, seats, lights and times by itself. Write only what happens and what's said; add `(face)`, moves and `[camera: ...]` only where the story needs them.
3. Rules that always apply: laugh with, never at; no sarcasm, no romance, no cringe; the four friends are boys; spooky not creepy; Friendzy appears naturally (real prompts only: `python3 prompts.py <game> 10`), never "download now"; a cold open grabs attention; the porch-light ending is automatic; fans must not be able to solve the secret.
4. Check in seconds, nothing voiced or rendered:
   `cd ~/Desktop/Friendzy/Blender/templates && python3 make.py episode --script ~/Desktop/Porchlight/episodes/epNN.txt --format horizontal --name epNN --check`
   It prints the length (aim 120-240 s), chapters, every shot and why, and lint (long lines, scenes with no physical business). Fix and re-check.
5. Show the user the script; scripts are approved in batches of 5. Record decisions in `DECISIONS.md`. Then stills (skill `render-episode`).

Cheap habits: one `--check` per draft, not per line; never render to test a script.
