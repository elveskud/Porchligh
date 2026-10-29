---
name: anim-body
description: Body mechanics and posing quality for Porchlight - line of action, weight, balance, walks, poses, hands, contact and props. Use when bodies look stiff, floaty, weightless, symmetrical or when choosing moves and poses.
---
# Body and posing

## Posing
- **Line of action**: one clear curve through the spine (`lean` bends the torso at the hips, `head_rot` continues it). Straight vertical bodies look dead; lean toward what the character wants.
- **Weight**: heavy Bash (roster weight 1.35) moves slower, lands harder, squashes deeper; light Pip (0.75) is quick and springy; Riot 1.0, Rocco 0.9 (slouched). Never give Pip Bash's timing.
- **Balance**: anything leaning far must be supported (a paw on something, a step, a wide stance) or be falling (trip).
- **Asymmetry**: different angles for each arm, one hand busy, weight on one side.
- Silhouette test: if the pose doesn't read as a black shape, open it up (arms away from body, head turned to profile).

## Walks and travel
- Any travel across the frame plays in the side view (`profile.py`) with the character's own cycle: Riot bouncy, Bash heavy, Pip quick small steps, Rocco loose and slouched. `runs in`, `sneaks off` change the gait.
- Feet stay planted: the side view puts the lower foot on the ground each frame; front-view walks use stride + bob. Sliding feet = a bug.
- Arrivals settle with a small overshoot; departures start with a dip and a look toward the exit.

## Drawn poses (poses.py) - use them, they're the biggest quality jump
`sits on the ground`, `lies on the beanbag` (whole scene); `kneels`, `trips`, `jumps into the lake` (cannonball), `climbs`, `runs at the camera`, `rests his chin in his paws` (per line). Seats on furniture are automatic with `"sit": "auto"`.

## Hands
- Shapes: paw, open, fist, point, thumbs, peace, three, four, horns, grab, hold. Hands match intent: point to accuse, open to explain, fist to resolve, grab to take, hold around props.
- Gestures land on stressed words; most lines need at most one gesture; Rocco and Pip gesture little.

## Contact and props
- Touches (`highfive`, `bump`, `hug`, `comfort`) step to arm's length and frame both; contact gets a small burst.
- Props: carried props sit in a `hold` paw; thrown/dropped props fly on arcs and, with Pymunk installed, really bounce and settle with a thud per bounce; water props splash.
- Things in hands react to the body (they shake on thunder, lag on turns).
