---
name: anim-review
description: Review stills or a render for animation quality like a supervising animator, and fix what's found in the cheapest way (script first, code last). Use after any stills run, before asking the user to approve, and whenever asked to "make it better".
---
# Quality review

Review the stills sheet (`--stills auto`: one still per shot) and `shots.txt` before showing the user. Fix what you find; then show.

## Checklist (look at every still)
**Readability**
- [ ] Is it clear who is talking and what they feel? Face visible, not cut by the frame edge, not under a caption (QA also checks faces).
- [ ] Silhouettes read; no limb hidden at the key moment; no tangents with set lines.
- [ ] One focus per shot; background life isn't louder than the acting.
**Acting**
- [ ] Faces match lines; no twinning (arms or characters in unison); listeners react but don't steal.
- [ ] Every scene has physical business; hands have jobs.
- [ ] Each character acts in their own signature (skill `anim-acting`).
**Motion (needs neighbouring frames: add stills 4-8 frames apart around a move)**
- [ ] Anticipation before big moves, overshoot and settle after; follow-through on ears/tails.
- [ ] Feet planted (no sliding); props in hands, not floating; contact in touches.
- [ ] Holds alive, not frozen; no popping (sudden jumps between consecutive frames).
**Staging and camera**
- [ ] 180-degree rule kept; eyelines match across cuts; shots at least ~1 s; cut points on action or on the line, not mid-gesture.
- [ ] Establishing shot in each new place; reaction shots where jokes land.
**World**
- [ ] Cast lit like the set; shadows and contact; colour consistent within a place; faces readable at night.

## Fix in this order (cheapest first)
1. Script: a face tag, a move, a pause, `to`/`look`, `(reaction X)`, a pose line, a camera override, split a long line. Re-run `--check`, then stills for just those frames.
2. Episode JSON fields (`ANIMATION_TODO.md`): seats, carry, pose, fx, grade.
3. Engine tuning behind `act` (skill `new-move`), then a reference sheet.
Never run a full render to judge a fix; stills of the affected frames only (`--stills 120,124,128 --reuse-voices`).

## Score before showing the user (be honest)
Clarity, acting, motion, staging, world: 1-5 each. Anything under 4 gets one more fix pass or is named in the report with what it would take.
