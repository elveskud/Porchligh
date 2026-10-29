---
name: blender-5-api
description: Facts and traps of the Blender 5.2 Python API as used headless by this pipeline. Use before writing or fixing any bpy code here, so it works first time.
---
# Blender 5.2 headless: what's true here (tested)

- Run: `/Applications/Blender.app/Contents/MacOS/Blender --background --python script.py` (env `BLENDER` overrides). **Blender exits 0 even when the script crashes**: always grep the output for `Traceback`/`Error` (make.py does).
- Renderer: `BLENDER_WORKBENCH`, flat shading, `color_type = "TEXTURE"`. EEVEE is `BLENDER_EEVEE` (there is no `BLENDER_EEVEE_NEXT` in 5.x).
- Image textures with alpha are dithered in Workbench: soft transparency (grain, haze) speckles. Use material `diffuse_color` alpha on flat meshes (`toon.light()`), or do it in ffmpeg (film grain is in make.py's encode).
- Keyframe interpolation: the preference isn't honoured in background renders; set `kp.interpolation = "CONSTANT"` on the F-curves. Actions are layered: `act.layers[].strips[].channelbags[].fcurves` (`episode_scene.fcurves_of()`).
- `toon.set_visible(o, vis, frame)` keys the object **and all children**: never use it on a character root (it would show every mouth and hand variant). Hide a whole character by keying `root.scale = (1e-4, 1e-4, 1)`.
- Copies get `.001` names: match with `name.split(".")[0]`.
- Grease Pencil is v3: `layer.frames.new(n).drawing`, `drawing.add_strokes([count])`, per-point `radius` (no `frame.strokes.new()`, no `line_width`). Line Art traces our flat cut-out cast badly: don't use it for the cast's outlines.
- Ortho camera: `sensor_fit = "VERTICAL"`, so `ortho_scale` = frame height in every format.
- Parallel jobs render frame ranges (`FRAME_RANGE`): anything random or time-based is computed from the absolute frame or a fixed origin, never from the job's first frame.
- `bpy.context.view_layer.update()` before reading `matrix_world` of things you just moved.
