# Blender pipeline: fixes and the auto-director (29 Oct 2026)

Made on a copy of the uploaded `blender-code.zip` and tested headless on Blender 5.2.3 (Linux) with placeholder
paintings, fonts and voices: Episode 1's scene (stills), a test episode that uses nearly every JSON feature
(stills), the audio mix, the thumbnail/cover, and a Shorts template (NHIE stills) as a regression check.
Nothing was rendered as a full video.

## How to apply
Unzip `blender-changed-files.zip` over `~/Desktop/Friendzy/Blender/` (it holds only the 15 changed or new files,
same folders), or `git apply blender-fixes.patch` inside the Blender folder. Then run `python3 doctor.py`.

## Bugs fixed
1. `doctor.py` reported ALL GOOD even when the cast code was broken (Blender exits 0 on script errors). It now
   fails properly, checks the Blender version is 5.x, and checks the Porchlight paintings exist.
2. `--reuse-voices` after editing a line kept the old voice forever. Now a later run without the flag redoes it.
3. Room tones dipped to near-silence at every change of place (measured 3-8% of their level). Now they overlap with
   equal-power fades, beats in the same place share one tone, and the 8 s loops no longer click or jump in volume
   every 8 seconds (the lake jumped about 9 dB).
4. Parallel renders (`--jobs`): blinks, twitches, eye darts, fidgets, tail sway, birds and leaves were timed from
   each job's first frame, so they jumped where jobs met. Now timed from the scene's start.
5. A render job starting more than ~33 s into a beat showed the wrong face, or crashed.
6. `scene.blend` from a parallel render only had the first job's animation. An extra job now bakes the whole
   episode while the others render.
7. Every parallel job ran Rhubarb on the same voices at once (4x the work, could corrupt the lip-sync cache).
   `make.py` now makes the cues once before rendering, and the files are written whole.
8. Group chats: bubbles could pop up after the beat ended and stay on screen in the next scene; 6+ bubbles ran off
   the bottom. Now the beat waits for the last bubble, and long chats scroll (4 on screen).
9. After a `walk_to`, cameras, looks and dust still used the old spot. Now they find the walker.
10. Emotes stayed where the character was placed (a "?" hung in the air while he walked in). They ride with him now.
11. Two new characters in one beat were given the same spot.
12. Close-ups counted the set's empty spots as bodies, so on a crowded set they backed out to a medium shot of
    everyone. (This also makes re-renders of Episode 1's apartment close-ups tighter.)
13. The title letters were evenly spaced, so the narrow I left gaps ("PORCHL I GHT").
14. Thumbnails on painted sets: a dark strip where the painting ended, day-lit characters on night sets, the badge
    running off the edge, and the dark cold open used as the default set. Fixed (it now uses the game scene).
15. Hard-coded paths: set `PORCHLIGHT_DIR` / `BLENDER` if the folders move; a missing painting gives a clear message.
16. The camera could drift back to an old shot during a line: a cut or push remembered "where the camera was" when it
    was added, so a move added later for an earlier frame (a line's own cut, added after its reaction cut; a camera
    move on a `quiet` line) left a stale position behind. Now worked out when the camera is baked.
17. Blender left a 10 MB `scene.blend1` backup in every re-rendered video folder (likely not covered by .gitignore).

## New
- **The JSON is checked before anything renders.** A typo in a name, move, camera, fx, side or an empty line
  stops with a message saying exactly what's wrong, instead of failing minutes into a render.
- **`"direct": "auto"` (the auto-director, `templates/director.py`).** For each line it decides who it's said to
  (the speaker turns to them), how hard it's played (from "!", SHOUTED words, "..."), and the shot: the beat opens
  on its own shot, two-way talk goes over the shoulder then to close-ups as it heats up, it pulls back to the room
  after four tight shots, never cuts faster than 1.2 s, and cuts to the listener's reaction on a line that lands.
  Every choice and its reason goes into `shots.txt` next to the video. Anything the script sets itself still wins.
- **`cu:who`**: a real head-and-shoulders close-up, with room on the side the character looks toward.
- **`label` fx**: words on the set (Ep 5's "12 August" on the calendar), so paintings stay free of text.
- `make.py` passes on the scene's WARNING lines (e.g. someone walking onto a spot that's taken).

## Last wins (107, 144, 146, 158, 175, 176, 198)
- A carried phone is held up in front, and the thumb taps between lines (with soft tap sounds).
- Night scenes: bigger pupil highlights (eye shine). Sunset: warm light bouncing up onto the legs.
- Close-ups (`cu`) get a little soft light on the face.
- A cushion thud when someone walks in and sits on a sofa, chair, bench or step.
- Thumbnails without a game use the episode's biggest line: its speaker yelling, the listener shocked.

## Feel pass (after the 200 wins)
- **Weight:** each character has a weight (Bash heavy, Pip light). Heavy hops are lower with a harder landing;
  heavy footfalls squash more.
- **Flinch:** when someone shouts, the others jolt back away from them and blink.
- **Eye contact:** characters look up at someone taller and down at someone shorter.
- **Handheld camera** in tense scenes; **an opening pan** across the painting when a scene moves to a new place.
- **`"grade"`** (summer, autumn, winter, faded) and **`"grain": true`** (soft film grain, added at the encode,
  also on stills). Screenplay headers `grade:` and `grain: on`.
- **Clothes rustle** on big moves.

## The big five (side views, poses, hands, world, open wins)
- **Side views** (`characters/profile.py`, approved): with `act`, every walk on, off and between spots is played by
  the side view with a real walk or run cycle (feet planted, own style per character) and a quick turn at each end.
- **Drawn poses** (`characters/poses.py`): cross-legged on the ground, kneeling, lying back on the beanbag, chin in
  paws, tripping, cannonball (into the lake: a splash and he's under), climbing, running at the camera.
  A dressed copy takes over for the pose with the same face, looks, blinks and lip sync.
- **Paws:** grab, hold (fingers round a carried cup, phone or flashlight), four; counting goes to five.
- **Faces:** brows and lids travel to a new expression over 5 frames; nervous and scared lines get a sweat drop.
- **World:** footprints in the sand, lamps flicker in storms.
- **Colour match** across sets in the same light, **`[silhouette]`** at sunset, **match cuts** between places.
- Reference sheets: `refs/side_*.png`, `refs/poses_*.png`, `refs/hands.png` (`sideref.py`, `poseref.py`, `handref.py`).

Everything new is opt-in from the episode JSON; the Shorts and Episode 1 behave as before (apart from the fixes).
