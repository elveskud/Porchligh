---
name: anim-principles
description: The 12 principles of animation mapped to exactly what the Porchlight engine does, with the numbers that make them read. Use whenever judging, writing or improving any animated moment, move or pose; the base for every other anim-* skill.
---
# The 12 principles, in this engine

The engine applies most principles automatically with `"act": "auto"` (motion.RICH). Your job: write scripts that give them room, and when building moves, honour every principle below. Frames are at 30 fps; the picture updates on twos (every 2nd frame), so anything shorter than 4 frames barely registers.

| Principle | What it means | Where it lives here | Rule of thumb |
|---|---|---|---|
| Squash & stretch | volume-preserving deformation shows weight and speed | `sq` channel (MUL; >1 tall-thin, <1 short-wide, volume kept), landings (`land` squash), takes, hops | squash 0.88-0.94 on impact, stretch 1.06-1.12 in fast motion; never change volume; heavy (Bash) squashes deeper, light (Pip) stretches more |
| Anticipation | a small opposite move before the main one | walk dip (8 frames), take wind-up, throw wind-up | 4-10 frames, 1/3 the size of the action, opposite direction; bigger action = longer anticipation |
| Staging | one clear idea per shot | auto-director shots, look room, spots staggered in depth | the eye goes where the contrast, movement and face are; only one character moves big at a time |
| Straight-ahead vs pose-to-pose | planned key poses vs continuous | moves are pose-to-pose curves (`motion.curve`) with springs on top | design the key poses first (extremes), then the timing between them |
| Follow-through & overlap | parts stop at different times | ear/tail springs, hoodie strings, head lag (`lean_lag`), elbow drag, hats lag | the body stops first, head 2-3 frames later, ears/tail/strings 4-10 frames later with one overshoot |
| Slow in / slow out | ease into and out of poses | `curve()` eases: smooth, out, in, back, elastic | ease "out" into holds; "back" for a snappy overshoot; "linear" only for mechanical things |
| Arcs | natural motion travels on curves | arm swings rotate at shoulder+elbow (arcs by construction), head bobs, thrown props are parabolas | never move a hand in a straight line across the body; tween via rotations, not positions |
| Secondary action | a smaller action that supports the main one | fidgets, tail wag on energetic lines, chip munch, phone taps, breathing | it must never compete: half the size and off the beat of the main action |
| Timing | the number of frames gives weight and mood | `episode_script` constants, move durations in `do_move` | fast = light/excited/funny; slow = heavy/sad/thoughtful (see anim-timing) |
| Exaggeration | push poses past real life | `motion.ACT` (global acting size), takes x1.25 with RICH, energy from punctuation | push the extremes, not the in-betweens; a pose should read as a silhouette |
| Solid drawing | volume and turning in space | head turns (TURN_PARTS), body narrowing on turns, side view (`profile.py`), drawn poses (`poses.py`) | turn the head before the body; use the side view for any walk across the frame |
| Appeal | clear, charming design and poses | the code-drawn cast, asymmetry (BROW_ASYM), squash in faces | asymmetry beats symmetry: one brow up, weight on one leg (lean), arms doing different things |

## Non-negotiables
- **No twinning**: both arms never doing the same thing at the same angle unless it's a deliberate gesture (clap, cheer). Neighbours never act in unison.
- **Moving holds**: nothing is ever frozen; idle breathing, drift, blinks and fidgets keep holds alive. A truly still frame reads as a bug.
- **Contrast**: a big move reads only next to stillness. After a take, hold. After a shout, the room goes quiet.
- **One focus**: the speaker acts, listeners react small (nod, glance, ear perk), never the reverse.
- **Everything opt-in**: new acting goes behind `RICH`/`ACT` so the Shorts and Episode 1 never change.
