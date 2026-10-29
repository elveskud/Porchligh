# Installing the pipeline update and rendering Episode 1 (on your Mac)

Everything here is typed in the **Terminal** app (Applications → Utilities → Terminal). Copy one block at a time,
paste it, press Enter, and wait until it finishes before the next one.

You need two files from the chat, saved in your **Downloads** folder:
- `blender-changed-files.zip`: only the files that changed or are new (24 code files + reference sheets)
- `Porchligh-docs-and-patch.zip`: the Porchlight notes (decisions, wins list, how to write an episode, Gemini prompts)

Nothing new needs installing: the update uses the same Blender, Python, ffmpeg and voices you already have.

---

## Step 1. Back up your current Blender folder

If anything goes wrong, you can put this copy back (step 9).

```bash
cp -R ~/Desktop/Friendzy/Blender ~/Desktop/Friendzy/Blender-backup-29oct
```

## Step 2. Put the changed files into the Blender folder

This copies the new and changed files over the old ones. Your voices, videos and everything else stay as they are.

```bash
unzip -o ~/Downloads/blender-changed-files.zip -d ~/Desktop/Friendzy/Blender
```

## Step 3. Check the setup

```bash
python3 ~/Desktop/Friendzy/Blender/doctor.py
```

It must end with **ALL GOOD**. If a line says BAD, it prints its own fix underneath. Do that fix, then run this step again.

## Step 4. Update the Porchlight notes (optional, until GitHub works)

Once GitHub access is fixed, you'll get these with a normal `git pull`, so you can skip this step. To have them now:

```bash
cd ~/Downloads && unzip -o Porchligh-docs-and-patch.zip
```
```bash
rsync -a --exclude episodes --exclude tools ~/Downloads/Porchligh/ ~/Desktop/Porchlight/
```

This adds and updates files and never deletes anything (your `episodes/` folder isn't touched).

## Step 5. Episode 1 exactly as it was approved: stills first

This makes about one still per camera shot. It takes a few minutes. Nothing is published anywhere.
(If your Episode 1 file has a different name than `ep01.json`, use that name.)

```bash
cd ~/Desktop/Friendzy/Blender/templates
```
```bash
python3 make.py episode --script ~/Desktop/Porchlight/episodes/ep01.json --format horizontal --name ep01 --stills auto
```

Then open the contact sheet:

```bash
open ~/Desktop/Friendzy/Blender/videos/ep01/stills_sheet.png
```

It should look like the Episode 1 you approved (this run checks that the update broke nothing).

## Step 6. Episode 1 with the new upgrades turned on

The upgrades are only on when the episode asks for them, so make a copy of Episode 1 that does:

```bash
cp ~/Desktop/Porchlight/episodes/ep01.json ~/Desktop/Porchlight/episodes/ep01_v2.json
```
```bash
open -e ~/Desktop/Porchlight/episodes/ep01_v2.json
```

TextEdit opens. Find the very first `{` at the top of the file, and right after it paste this line:

```
"direct": "auto", "act": "auto", "sit": "auto", "grade": "summer", "grain": true,
```

Save (Cmd+S) and close.

What each switch does:
- `direct`: the auto-director picks the shots: reaction cuts, close-ups, cuts on actions. Cameras you set yourself in the episode still win.
- `act`: the automatic acting: gestures from the words, listeners react, weight, flinches, eye contact.
- `sit`: everyone sits on the set's seats by themselves.
- `grade`: the colour grade (summer, autumn, winter or faded).
- `grain`: a soft film grain.

To leave one out, delete it from the line, keeping the commas between the others. A typo stops with a message,
not a broken video.

Check it in seconds (nothing is voiced or rendered). This prints the length and every shot the director picked:

```bash
python3 make.py episode --script ~/Desktop/Porchlight/episodes/ep01_v2.json --format horizontal --name ep01_v2 --check
```

Then the stills:

```bash
python3 make.py episode --script ~/Desktop/Porchlight/episodes/ep01_v2.json --format horizontal --name ep01_v2 --stills auto --reuse-voices
```
```bash
open ~/Desktop/Friendzy/Blender/videos/ep01_v2/stills_sheet.png
```

Compare it with step 5's sheet. Send me both sheets here in the chat if anything looks off.

## Step 7. The full video

Only once the stills look right. On the M3 this takes about 8–11 minutes for a 3–4 minute episode.

```bash
python3 make.py episode --script ~/Desktop/Porchlight/episodes/ep01_v2.json --format horizontal --name ep01_v2 --jobs 6 --reuse-voices
```

## Step 8. Check the result

```bash
open ~/Desktop/Friendzy/Blender/videos/ep01_v2
```

That folder has:
- `ep01_v2.mp4`: the episode, plus a silent copy
- `qa.txt`: the automatic checks (length, loudness, black gaps, silence, faces too dark or covered by captions). It should say everything passed; if not, it says what and where.
- `qa_sheet.png`: one frame every few seconds
- `chapters.txt`: YouTube chapters
- the 1280×720 thumbnail
- `shots.txt`: every camera decision and why

Nothing is uploaded or posted.

## Step 9. If something goes wrong: go back to the old version

```bash
rm -rf ~/Desktop/Friendzy/Blender && mv ~/Desktop/Friendzy/Blender-backup-29oct ~/Desktop/Friendzy/Blender
```

Then send me the last 20 lines the Terminal printed, and I'll fix it.

---

**Not in this update yet** (next on the list): the approved side-view walks inside episodes, the new poses
(beanbag, cross-legged, kneeling, tripping, chin in paws) and the new paw shapes. Right now they only exist as the
reference sheets in `Blender/characters/refs/side_*.png`.
