---
name: set-tools
description: Use the set and physics tools - depth layers, moving parts cut out with Segment Anything 2, real prop physics with Pymunk. Use when a set needs depth for camera moves, doors/trees/curtains/lamps that move, or when props should bounce realistically.
---
# Set and physics tools (all free for commercial use)

- **Depth layers** (`Blender/tools/depth_layers.py`, guide `DEPTH_LAYERS.md`): `python3 depth_layers.py <img>` with Gemini F3 pictures, or `--bands y1,y2` (painting px, cut at the horizon/shore). Check `art/hd/sets/layers/<img>_layers.png` and `_parallax.gif`. Mean difference over ~28 = regenerate the Gemini picture. Episodes with `act` use the layers automatically.
- **Moving parts** (`Blender/tools/cutout.py`, Segment Anything 2, Apache-2.0; needs torch + transformers): `python3 cutout.py <img> --find` writes a numbered sheet, then `--keep 7:door:door,12:tree:sway`; or `--point name:kind:x,y`; or `--mask name:kind:file.png` (a hand mask or a Gemini F2 magenta picture). Kinds: sway, door, flicker, spin, front. Check `art/hd/sets/parts/<img>_parts.png`. **Not yet built:** the pipeline side that loads and animates these parts in episodes (as of 29 Oct the tool only makes the cut-outs, the clean plate and the JSON).
- **Prop physics** (`Blender/characters/physics2d.py`, Pymunk, MIT): `pip install pymunk` into the python3 that runs make.py. Throws and drops then bounce, tumble and settle, with a thud on each contact, worked out once in `episode_script.py` and stored in cues.json (Blender itself doesn't need Pymunk). Without it, the old cartoon hops are used.
- Licences rule (`DECISIONS.md` round 15): only tools free for commercial use; Depth Anything only in its Small model; no MoMask; nothing that needs the user to act or film.
- The cloud session can't download model weights (huggingface.co is blocked there): run SAM 2 on the Mac.
