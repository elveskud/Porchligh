---
name: anim-timing
description: Timing and spacing for Porchlight - frame counts for moves, holds, pauses, comedic timing, easing choices, twos vs ones. Use when a moment feels rushed, slow, floaty, stiff or unfunny, or when building a new move.
---
# Timing and spacing (30 fps, drawn on twos)

## Reference durations (frames)
| Action | Frames | Notes |
|---|---|---|
| blink | 3-4 (slow blink 8) | blinks hide expression changes; one every 2-4 s |
| eye dart | 2-3 move, hold 6+ | eyes lead the head by 2-3 frames |
| head turn | 6-8 | body follows 3 frames later |
| expression change | 2 (5 with act) | change on a blink when possible |
| anticipation | 4-10 | longer for bigger actions |
| take (shock) | 3 up, hold 8-14, settle 10 | the hold sells it |
| double take | look away 10, snap back 4 | |
| hop | 22 (heavier = longer) | |
| nod / shake | 8 per nod, 2-3 nods | |
| step (walk) | 10-13 per step | Riot 10, Pip 8 (quick), Bash/Rocco 13 |
| run step | 6-8 | |
| walk on/off | 45 (motion.WALK) | |
| throw | release 8, flight 20 | the landing frame is where the sound goes |
| silent beat (`NAME: ...`) | 36 | |
| reaction after a punchline | 8-14 frames before it starts | |

## Holds and pauses
- A pose needs at least 6-8 frames on screen to register; important poses 12-24.
- Comedy: setup → beat (8-15 frames of stillness) → punchline → hold (12-20) → reaction. The pause is where the laugh lives. Use `[hold: 0.5]` or a silent line for the beat.
- Never cut away during a take's hold; let the reaction finish before the next line.
- Drama: slower. 1-2 s pauses before emotional lines are fine.

## Spacing and easing
- Close spacing = slow (near poses); wide spacing = fast (middle of a move). Ease out of the start, ease into the end (`smooth`), overshoot with `back`, wobble with `elastic` (for springy cartoon settles only).
- Fast moves over 2-4 frames read as snaps; give them a smear (paws stretch on fast swings) or a squash on the stop.
- Linear motion is only for machines, camera drift and falling things before impact.

## Twos and ones
- Everything renders on twos (classic 2D, and half the render time). Very fast actions can strobe on twos: keep fast moves to clear key poses and let squash/smear carry the speed. `--ones` renders every frame (slower; for special episodes).

## Rhythm of a scene
- Vary line lengths and gaps; three lines of identical length and spacing feel robotic.
- Fast exchanges: overlapping looks, quick cuts (the director holds both in a two-shot if cuts would come faster than 36 frames).
- After a big moment, slow down. After a slow stretch, a quick beat wakes the viewer.
