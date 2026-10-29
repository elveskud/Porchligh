# Porchlight

An animated story series set in Maple Hollow, a lake-and-forest town where summer never ends. Riot, Rocco, Bash and Pip (the Friendzy cast) are the main characters. 40 episodes of 3–4 minutes, landscape, released Wednesday and Saturday.

This is its own project, separate from the Friendzy advertiser (which only makes Shorts, carousels and stories).

## What's here
| File | What it is |
|---|---|
| `DECISIONS.md` | Every decision made with the user so far. Read this first. |
| `archive/old-series-idea/` | The earlier "Campfire Confessions" series idea (SERIES.md + its test episode JSON). Rejected; kept for reference only. |

Coming next: `BIBLE.md` (world, cast, rules of the secret), `STORY_MAP.md` (all 40 episodes, one paragraph each), then `scripts/` (full episode scripts, in batches of 5).

## What lives elsewhere
- **Animation pipeline:** `~/Desktop/Friendzy/Blender/` (shared with the Shorts). Episodes are rendered with the `episode` template: `python3 make.py episode --script <episode>.json [--format horizontal]`. JSON format: `Blender/README.md` section 5; example: `Blender/templates/examples/campfire-confessions/ep01.json`.
- **Characters and voices:** `~/Desktop/Friendzy/Blender/characters/` and `Blender/voices/`.
- **Shorts, carousels and stories:** the advertiser agent in `~/Desktop/Friendzy/.claude/agents/advertiser.md`. It doesn't touch this project.

## Rules for working on it
- UI and dialogue in English; family-friendly (teens and adults), no cringe, no sarcasm.
- Videos are Blender 2D only; sounds, voices and music are generated.
- While building pipeline pieces, prove them with stills, not full renders.
- Nothing is posted, scheduled or pushed without the user asking.
