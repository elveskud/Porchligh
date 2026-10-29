# Porchlight

An animated story series set in Maple Hollow, a lake-and-forest town where summer never ends. Riot, Rocco, Bash and Pip (the Friendzy cast) are the main characters. 40 episodes of 3–4 minutes, landscape, released Wednesday and Saturday.

This is its own project, separate from the Friendzy advertiser (which only makes Shorts, carousels and stories).

## What's here
| File | What it is |
|---|---|
| `DECISIONS.md` | Every decision made with the user so far. Read this first. |
| `BIBLE.md` | The series bible: world, cast, the secret and its rules, tone, Friendzy's place. Approved 28 Oct (round 7). |
| `STORY_MAP.md` | All 40 episodes, written one arc at a time. Arc 1 approved (round 9); arc 2 written, open questions at its end. |
| `ANIMATION_CHECKLIST.md` | The animation rules (dos and don'ts), the known problems with their status, and the per-episode checklist. |
| `ANIMATION_TODO.md` | The first 37 animation fixes, and every episode JSON field the Porchlight pipeline understands. |
| `GEMINI_PROMPTS.md` | Prompts for the Gemini set paintings (in the cast's style). |
| `CLAUDE.md` | How to work on this project (for Claude sessions). |
| `pipeline-patches/` | Changes to the shared Blender pipeline waiting to be applied on the Mac (`blender.patch` + `CHANGES.md`). |

Not in this git repo: the art (`art/`), `episodes/` and `tools/` folders, which are in the local `~/Desktop/Porchlight` folder, and the rejected "Campfire Confessions" idea (`archive/old-series-idea/`).

Coming next: the full scripts (`scripts/`, in batches of 5) once the story map is approved, then each approved script as episode JSON (`episodes/`).

## What lives elsewhere
- **Animation pipeline:** `~/Desktop/Friendzy/Blender/` (shared with the Shorts). Episodes are rendered with the `episode` template: `python3 make.py episode --script <episode>.json [--format horizontal]`. JSON format: `Blender/README.md` section 5; example: `Blender/templates/examples/campfire-confessions/ep01.json`.
- **Characters and voices:** `~/Desktop/Friendzy/Blender/characters/` and `Blender/voices/`.
- **Shorts, carousels and stories:** the advertiser agent in `~/Desktop/Friendzy/.claude/agents/advertiser.md`. It doesn't touch this project.

## Rules for working on it
- UI and dialogue in English; family-friendly (teens and adults), no cringe, no sarcasm.
- Videos are Blender 2D only; sounds, voices and music are generated.
- While building pipeline pieces, prove them with stills, not full renders.
- Nothing is posted, scheduled or pushed without the user asking.
