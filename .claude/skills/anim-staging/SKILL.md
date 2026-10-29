---
name: anim-staging
description: Staging, composition and camera for Porchlight - shot choice, framing, eyelines, the 180-degree rule, depth, cuts and camera moves, and when to override the auto-director. Use when shots feel confusing, flat, cramped or dull.
---
# Staging and camera

The auto-director (`templates/director.py`, `"direct": "auto"`) already does: establishing wide, shot/reverse over the shoulder, close-ups as an exchange heats up, re-orienting wides after 4 tight shots, cut on action, two-shots for touches, wide for throws, reaction close-ups, snap-ins on shouts, slow creep on long holds, dutch angle in tense beats, follow pans on walks, wide for exits, opening pans in new places, match cuts between places. `shots.txt` (and `--check`) lists every choice and why. Override only with a reason: `[camera: close riot]` locks the scene's camera; a line's own `camera` wins for that line.

## Composition
- Rule of thirds for faces in close-ups; **look room**: the face sits off-centre away from where it looks (automatic in `cu`).
- Headroom: eyes about 1/3 from the top in close shots; never cut at joints (neck, waist, knees) - frame mid-chest or mid-thigh.
- Silhouette readability: a pose must read as a black shape. Arms away from the body, profile for walks, no limbs hidden behind the torso at key moments.
- Avoid tangents: a character's outline touching a set line (horizon, door edge) flattens depth; nudge the spot or the camera.
- Depth: the 4 standing spots step back alternately (smaller, higher); use front/back to show who matters. Foreground pieces (fronts, near depth layer) frame the shot.

## Continuity
- **180-degree rule**: keep each character on the same side of the frame within a scene. The engine's sides come from spot positions; don't swap seats mid-scene without a walk.
- Eyelines match across cuts: if Riot looks right at Bash, Bash looks left at Riot (automatic with `to`/`look`). Height-correct eye contact is automatic with act.
- Screen direction: someone exiting right enters the next place from the left.

## Camera moves
- Every move needs a motive: follow action, reveal, or intensify emotion (slow push-in on quiet lines). Avoid moving and cutting at once.
- Push-ins for importance, pull-backs for isolation/reveal, handheld for tension (automatic in tense beats), shake only on impacts.
- Hold a shot at least 36 frames (MIN_SHOT); under 1 s reads as a jump (flagged in shots.txt).

## Shot choice cheat sheet
| Moment | Shot |
|---|---|
| new place / time jump | wide (opening pan), or a match cut if someone carries over |
| two talking | over-the-shoulder, then close-ups as it heats up |
| a joke landing | snap-in on the speaker, then the listener's reaction close-up |
| a secret / emotion | slow push-in, close-up, `quiet` |
| physical comedy / throws / walks | wide or two-shot, never a close-up |
| a group decision | wide with a lean toward the speaker (`favor`) |
| a detail (photo, calendar) | insert (`at:`), creeps in |
