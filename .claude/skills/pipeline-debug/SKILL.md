---
name: pipeline-debug
description: Find and fix a failing or wrong-looking Porchlight render quickly and cheaply. Use when make.py errors, a still looks wrong, QA fails, or doctor.py reports BAD.
---
# Debugging the pipeline

1. `doctor.py` first; follow its printed fix for any BAD line.
2. Script/JSON problems stop early with a message naming the beat and field (`check_beat` in `episode_script.py`); fix the script, re-run `--check`.
3. A crash inside Blender: the Traceback is in make.py's output (Blender itself exits 0). Reproduce with the fewest frames: `--stills <one frame> --reuse-voices`.
4. A wrong-looking frame: render just that frame as a still and compare with the same frame before your change (pixel diff with PIL). Never run a full render to look at one problem.
5. Common causes: something hidden with `set_visible` on a character root; a key on one parallel chunk only (not deterministic per frame); a camera `cut` and `push` at the same frame (remove the plain cut first: `CA.keys = [k for k in CA.keys if k[0] != f]`); a scale/visibility key that the bake overwrote (key after the bake); a set file missing (`PORCHLIGHT_DIR`).
6. Before handing back: run an old-style episode (`templates/examples/campfire-confessions/ep01.json`) to stills and confirm it's pixel-identical, so the Shorts and Episode 1 didn't change.
