---
name: render-episode
description: Make stills or the final video of a Porchlight episode safely, with the approval gates. Use when the user asks to render, preview, make stills, or finish an episode.
---
# Rendering an episode

Order is fixed: doctor, stills, user OK, full render. Never render an unapproved episode; never post, schedule, commit or push unless asked.

1. `python3 ~/Desktop/Friendzy/Blender/doctor.py` must end with ALL GOOD (each BAD line prints its fix).
2. Stills (one per shot), from `~/Desktop/Friendzy/Blender/templates`:
   `python3 make.py episode --script <ep>.txt --format horizontal --name epNN --stills auto`
   Show `../videos/epNN/stills_sheet.png` to the user. Add `--reuse-voices` on reruns (voices are slow).
3. After the user's OK, the full video (~165 s of render per minute of video on the M3):
   `python3 make.py episode --script <ep>.txt --format horizontal --name epNN --jobs 6 --reuse-voices`
4. Read `../videos/epNN/qa.txt`: length 120-240 s, -14 LUFS, no black gaps, no dead air over 1.2 s, faces not dark or under captions. Report the mp4 path and anything QA flags.

Outputs in `Blender/videos/epNN/`: mp4 (+ silent), `qa.txt`, `qa_sheet.png`, `stills_sheet.png`, `shots.txt`, `chapters.txt`, the 1280x720 thumbnail.
Cloud sessions have no real voices or paintings: renders there only prove code, never judge the look there.
