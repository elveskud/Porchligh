---
name: new-move
description: Add a new acting move, pose, gesture or effect to the animation pipeline without changing anything that already works. Use when a script needs an action the engine doesn't have (see WRITING_AN_EPISODE.md for what exists).
---
# Adding a move or pose

1. Check it doesn't exist: `WRITING_AN_EPISODE.md`, `screenplay.MOVES`, `poses.ALL`, `characters/refs/moves_sheet.png`.
2. Where it goes:
   - acting from the standing rig: a function in `characters/motion.py` returning channels via `a.add(lambda fr: {...})` (channels: x, y, rot, lean, head_rot, head_y, turn, ears, tail, stride, kneel, sq, armS/elbowS/handS, faceS, reachS...);
   - something the rig can't bend into (folded legs, lying): a drawn pose in `characters/poses.py` (`dress()` parts + `layer()` channels);
   - an effect in the world: `templates/episode_scene.py`.
3. Wire it: `screenplay.MOVES` (+ an action phrase in `_action` if natural), `do_move()` in `episode_scene.py` (with its `end` duration), sounds in `episode_script.py`'s foley loop if any.
4. Everything new is opt-in: only with `"act": "auto"` (`motion.RICH` / `ACT`), so the Shorts and Episode 1 never change. Deterministic per absolute frame (renders run in parallel chunks); no `random` without a seed from the frame.
5. Prove it on a sheet, not a render: `movesheet.py` / `poseref.py`, or a 2-line script with `--stills`. Show the user.
