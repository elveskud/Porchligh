---
name: gemini-art
description: Get pictures from Gemini (set paintings, angle and pose guides, depth layers, cut-outs) and use them correctly. Use when a set, a pose or a reference is needed that only a picture can give.
---
# Working with Gemini pictures

- Gemini paints sets only. For the cast it gives guides (angle, pose) that are copied in code; its drawings never appear in episodes. It often drifts off-model (wrong colours, extra patches): ignore those details.
- Prompts live in `GEMINI_PROMPTS.md`: A fixes, B reverse angles, C new sets, D townsfolk, E cast guides (attach `refs-for-gemini/<name>.png` as image 1), F moving parts and depth layers. Always add "Exactly the same size, framing and position as image 1" when editing a painting.
- The user uploads up to 5 pictures per message. Pictures sent while a turn is running are visible but not saved as files: ask them to keep copies in `~/Desktop/Porchlight/art/gemini/` and to resend if a file is needed.
- File names: `art/gemini/sets/<img>_far.jpg|_mid.png|_near.png` (depth), `art/gemini/refs/turnaround_<name>.jpg`, `walk_<name>.jpg`, `poses_<name>.jpg`, `paws_<name>.jpg`.
- Magenta (#FF00FF) means empty in cut-out pictures; the tools key it out.
