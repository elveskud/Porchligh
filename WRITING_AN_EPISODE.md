# Writing an episode (the plain-text script)

An episode is a plain `.txt` file in `episodes/`. The pipeline turns it into the episode JSON (written beside it as
`epNN.json`), directs it (shots, reaction cuts, who talks to whom, how hard each line is played) and renders it.
Anything you write yourself wins over the engine's choices.

```
# Porchlight 2: Dare House
next: Summer Homework
thumb: DON'T TOUCH IT

== Cold open | hall, night | riot
[text: Maple Hollow. Late.]
RIOT carries a flashlight.
RIOT (determined, whispers): Again.

== The dare | lake, day | riot (lifeguard), rocco, bash, pip
BASH enters left.
[game td: Touch the door of the haunted house. | bash | Easy.]
BASH (nervous): Easy. Totally easy.
ROCCO: ...
```

## The pieces
| Write | What it does |
|---|---|
| `# Porchlight 2: Dare House` | series, episode number, title (first line) |
| `next:` / `previously:` / `thumb:` | the next episode's name, a recap line, 2–4 thumbnail words |
| `grade: summer` / `grain: on` | the episode's colour grade (summer, autumn, winter, faded; lighter at night) and a soft film grain |
| `== Chapter \| place, time \| who (costume), who` | a new scene. Places: lake (day/night), stoop (sunset/night), apartment, hall. A change of time of day fades through black. The first scene gets letterbox bars (the cold open). |
| `NAME: words` | a line |
| `NAME (nervous): words` | a face: happy, hype, cocky, shocked, nervous, suspicious, sad, soft, scared, embarrassed, determined, yelling, smug, pouting, sleepy... |
| `NAME (take): words` | a move: take, laugh, cheer, nervous, yell, shrug, facepalm, wave, thumbs, present, hop, double_take, point, munch, fan, shiver, stare, cross, hips, nod, shake, clap, count, peace, horns, rock, gloom, yawn, stretch, scratch, chuckle, crouch, pockets, lean, slouch (see `Blender/characters/refs/moves_sheet.png`) |
| `NAME (whispers): words` | a quiet, emotional line (also `quietly`, `softly`) |
| `NAME (joke): words` | a punchline: snap zoom and a soft sting |
| `NAME (to pip): words` / `(looks up)` / `(looks at bash)` / `(reaction rocco)` | who it's said to, where they look, whose face we cut to after |
| `NAME: ...` | a silent beat: acted (face, look, move), not voiced |
| `NAME enters left.` / `NAME exits right.` | walking on and off |
| `NAME walks to the step.` | walking to another spot mid-scene |
| `NAME sits on the sofa l.` / `stands at the tower.` | where they are (otherwise sitters take free seats on their own) |
| `NAME is asleep.` / `NAME carries a phone.` | asleep for the scene / a phone, flashlight or cup in the paw (a phone is held up and tapped between lines) |
| `RIOT high-fives BASH.` / `bumps` / `hugs` / `puts a paw on PIP's shoulder` | two of them touching: they step to arm's length, the camera takes a two-shot |
| `BASH picks up the cup.` / `puts down` / `throws it at the lake` / `drops` / `sips` | props: thrown things fly, bounce and splash |
| `[text: ...]` `[card: Later that night.]` `[sfx: door]` | on-screen text, a time card, a sound |
| `[storm]` `[fade]` `[whip]` `[letterbox]` `[mood: tense]` `[hold: 2]` | weather, transitions (fade through black, whip pan), the scene's mood (`normal`, `tense` tilts the camera, `party`, `soft` = piano), seconds to hold at the end |
| `[intro]` | the Porchlight title with the full theme |
| `[camera: close riot]` | frame the scene yourself (the engine then leaves this scene's camera alone) |
| `[chat]` then `Riot: LIGHT'S ON` lines, then a blank line | the group chat |
| `[game nhie: prompt \| target \| confession]` | Never Have I Ever (also `mlt: prompt \| target`, `td: dare \| player \| performance`). Real app prompts only. |
| `[json: {...}]` | anything else from `ANIMATION_TODO.md`, as JSON |
| `--` | a new beat in the same scene |
| `// note` | a comment |

## Checking a draft in seconds
`python3 make.py episode --script ../../Porchlight/episodes/ep02.txt --format horizontal --check` prints the length,
the chapters, every shot the engine picked (and why), and anything it noticed (very long lines, scenes where
nobody does anything physical). Nothing is voiced or rendered.
