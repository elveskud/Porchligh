---
name: new-set
description: Add a new painted set (location) to Porchlight, from Gemini painting to usable episode location with spots, light, depth and moving parts. Use when a script needs a place that isn't one of lake, lake_night, stoop_sunset, stoop_night, apartment, hall.
---
# Adding a painted set

1. Painting: prompt from `GEMINI_PROMPTS.md` (section C, or write one in the same style: attach `lake_day_v2` as the style reference; no characters, no text, 16:9). The user makes it and uploads it here (5 pictures per message).
2. Save the 4K plate as `~/Desktop/Porchlight/art/hd/sets/<img>.png` (3840x2160). Upscale small Gemini output first (Real-ESRGAN anime model is free, BSD-3).
3. Register it: a new entry in `locations.PLATE_SETS` (`Blender/characters/locations.py`):
   `"<set>": dict(img="<img>", ground=<px>, xs=(4 standing x px), s=0.48, tint=(col, a), cast=(col, a), shadow=(alpha, stretch, dx), haze=col)`.
   All positions are painting px in 1024x572 space. Night sets: cast alpha > 0.3. Add it to `screenplay.py`'s place names if it has a short name.
4. `art/hd/sets/<img>.json`: `spots` (named seats `[px, py, "sit"|"stand", scale, z]`), `life` (copy keys from a similar set), `lamps` (`[px, py, col, radius_px, strength]`), `fronts`.
5. Optional depth and moving parts (skill `set-tools`).
6. Prove it with stills only: a 2-line test script in the new place, `--stills 10,60`. Show the user before any episode uses it.
Never change an existing set's numbers for a new one; add, don't rewrite.
