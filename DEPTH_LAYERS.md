# Depth layers for painted sets (guide for the user and for Claude)

A painted set is one flat picture, so when the camera moves, everything in it moves together. Splitting it into
**far / mid / near layers** that slide at different speeds gives real depth: hills drift slowly, the ground the cast
stands on stays put, grass in front sweeps past. This page is the whole process. The tool is
`~/Desktop/Friendzy/Blender/tools/depth_layers.py`; the pipeline uses its output by itself.

## What the layers are
| Layer | What's in it | Moves | Where it sits |
|---|---|---|---|
| far | sky, clouds, far hills, the far shore: everything behind the ground | 0.82× the camera (trails it) | behind everything |
| mid | the ground the cast stands on: beach, floor, street, dock, water | 1× (stays put, so feet stay planted) | behind the cast |
| near | the nearest things along the bottom edge: grass, rocks, a railing | 1.22× (runs ahead) | **in front of the cast** |

Rules that make it work:
- **The cast's ground is always mid.** If the near layer includes ground someone stands on, run the tool with
  `--near-behind` (the near layer then sits behind the cast).
- **Cut along natural edges** (the horizon, a shoreline, the base of a wall). A cut straight across a painted
  object shows as a seam when the layers slide.
- Layers only add depth when the camera moves: the opening pans, push-ins (a push-in also grows near things more
  than far ones), creeps, follow pans, match cuts.

## Step by step

### 1. Make the pictures (Gemini, best)
Use `GEMINI_PROMPTS.md` F3 with the set's painting as image 1. Save the three results as
`art/gemini/sets/<img>_far.jpg`, `<img>_mid.png`, `<img>_near.png`, where `<img>` is the painting's name in
`locations.PLATE_SETS` (lake → `lake_day_v3`, lake at night → `lake_night_v2`, stoop at sunset →
`stoop_sunset_v2`, stoop at night → `stoop_night_v2`, apartment → `apartment_night_v2`, hall →
`hall_inside_night_v2`).

What matters in Gemini's pictures:
- far: nothing near left in it; the sky and hills continue where the ground and grass were.
- mid and near: **pure magenta (#FF00FF)** everywhere else, with no shading or gradient in the magenta.
- Same framing as the painting. Small shifts, scale changes and a different picture size are fine (the tool fixes
  them). Repainted *shapes* are not: if a hill moved, ask again.

### 2. Run the tool
```bash
cd ~/Desktop/Friendzy/Blender/tools
```
```bash
python3 depth_layers.py lake_day_v3
```
It takes 1–2 minutes and prints how it lined each picture up:
`mid: scale 0.986 (width x0.994), shift (+24, -16) px, mean difference 5.7`.
- **mean difference under ~15**: good.
- **15–28**: check the sheet carefully.
- **WARNING over 28**: Gemini moved or redrew too much. Ask again ("exactly the same size and position as image 1,
  do not move anything"), or use step 2b.

**2b. No Gemini pictures?** Cut the painting at two heights (painting pixels, 1024×572 like every set JSON:
y = 0 at the top):
```bash
python3 depth_layers.py lake_day_v3 --bands 360,530
```
Above 360 = far, 360–530 = mid, below 530 = near. The hidden parts are filled by mirroring, which is fine for
small camera moves. Pick the heights at natural edges (the horizon, the shore).

### 3. Check it before any render
The tool writes to `art/hd/sets/layers/`:
- `<img>_layers.png`: the painting, then each layer on a checkerboard. Look for **magenta or pink anywhere**,
  holes in the far layer, and halos round near things.
- `<img>_parallax.gif`: the layers sliding in a camera pan. It should feel like looking past the grass at the
  water and hills, with nothing tearing or smearing.
- `<img>.json` gets `"layers": {"far": 0.82, "near": 1.22, "near_behind": false}`. Change the two numbers for
  more or less depth (0.7 / 1.35 is strong; 0.9 / 1.1 is subtle). Delete the key to switch layers off for this
  set.

### 4. See it in an episode (stills)
Any episode with `"act": "auto"` uses the layers automatically. A quick test still pair, with a push-in:
```
# Porchlight 0: Depth test
== Lake | lake, day | riot, bash
[json: {"move": "close:riot"}]
RIOT: Look how far the water goes.
BASH: All the way to the hills.
```
```bash
python3 make.py episode --script depth.txt --format horizontal --name depth --stills 8,150
```
Frame 8 is wide, frame 150 pushed in. Hills and water should have moved less than the beach, and the grass more.

## How the tool works (for Claude, when changing it)
1. **Gemini's pictures are trusted for shapes, never colours.** Every layer is cut from the painting's own pixels
   with masks from Gemini's magenta. Gemini's pixels are only used where the painting has nothing: the sky and hills
   behind the ground (in the far layer, colour-matched to the painting first). The ground behind near things is
   filled from the painting's own ground around them (normalised-convolution inpaint), because only slivers of it
   ever show.
2. **Alignment:** each picture is stretched to the plate's size (Gemini keeps the composition but returns its own
   size), then a coarse-to-fine search over scale, width stretch and shift. It minimises the mean colour difference,
   with these safeguards:
   - only inside solid paint, at least a pixel in from any edge (blended magenta edges read as solid pink, and thin
     layers like grass are nearly all edge);
   - each pixel's difference is capped at 40, so a border or something Gemini added can't outvote the rest;
   - the uncovered border after a shrink is magenta (empty), never black.

   The near and far layers start from the mid layer's fit (Gemini moves all three alike) and only refine it.
3. **Masks:** specks removed, grown 4 px (a little background rides along, so no gap shows round an edge), feathered
   1.5 px, and carried out to the frame edge where the fitted picture didn't reach.
4. **Pipeline:** `locations.plate()` loads `layers/<img>_far|mid|near.png` when the set JSON has `"layers"` and the
   episode has `act` (`locations.PARALLAX_LAYERS`):
   - far is the plate object (`<set>_plate`, z -9.5, so the close-up soft background still works);
   - mid sits at z -9.38;
   - near sits at z 9.1 (in front of the cast), or -9.36 with `near_behind`.

   Far and near join `L.parallax` with their factors and `depth_zoom`. `episode_scene.py`'s parallax pass slides
   them with the camera, and for `depth_zoom` layers also scales them about the camera centre on push-ins
   (`(13.5 / ortho) ** (0.5 × (factor − 1))`).

Tested here on a synthetic painting with known damage (shift +24/−14 px, 2 % scale, a squashed 1408×768 size,
a colour tint): it recovered the fit to within about 2 px, with mid/near differences of 1.1 and 3.5. Not yet tried on
a real Gemini F3 set: the first real run is the true test, so check the sheet and GIF.
