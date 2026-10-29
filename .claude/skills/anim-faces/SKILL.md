---
name: anim-faces
description: Facial animation and lip sync quality for Porchlight - choosing expressions, eye acting, blinks, brows, pupils, mouths, sweat and blush. Use when faces look flat, wrong for the line, flickery, or when close-ups matter.
---
# Faces

## The expression set (cast.EXPRESSIONS)
| Feeling | Use | Notes |
|---|---|---|
| happy, soft | warm, content; soft = quiet/wistful | soft has eyes a little down |
| hype, laughing | excited, laughing | laughing uses ^ ^ eyes (no blinks) |
| cocky, smug, side_eye_l/r | confident, teasing, "told you" | asymmetric brows; Riot's home faces |
| suspicious, deadpan | doubt; Rocco's resting face | half-lidded |
| shocked, scared | surprise; fear | tiny pupils (scared smallest) |
| nervous, embarrassed | worry; caught out (cheeks flush) | Pip's home faces; sweat drop with act |
| yelling, determined, drumroll | anger/outrage; resolve; suspense | yelling flushes red; Bash's home face |
| sad, pouting | sorrow; sulking/begging | big eyes for pouting |
| sleepy, asleep, disgusted | tired; sleeping; "ew" | |

## Rules
- The face changes before the line (thought first). With act, brows and lids travel over 5 frames; the change gets a blink to hide the mouth swap.
- Hold an expression at least 12 frames; flicking between faces reads as twitching.
- Eyes carry most of it: where they look (`to`, `look`), how open (squash per expression), pupil size (shrink in fear, grow when excited or begging), blinks (slower in sleepy/smug/sad).
- Eye darts before speaking and a glance away mid long line are automatic; don't over-add `looks` tags.
- Asymmetry reads as thought: suspicious/smug/cocky raise one brow automatically.
- Laugh with, never at: when someone is teased, their face goes embarrassed → laughing within the scene.

## Lip sync
- Rhubarb mouth shapes from the generated voice, one frame ahead of the sound with act (reads in sync), closed M/B/P shapes kept, mouths on twos. Loud syllables stretch the mouth and drop the jaw by line energy.
- Write lines that sound natural aloud; mumbled or clipped text gives mushy mouths. Punctuation sets energy: "!" bigger, a SHOUTED word biggest, "..." softer.
- Side view (walking) has no lip sync: avoid long lines during walks; put the line after arrival.

## Extras
- Sweat (nervous/scared), flush (yelling red, embarrassed pink), dread lines (shock), sparkles/emotes (`emote` in JSON: sweat, anger, sparkle, question, exclaim, heart, zzz). Use emotes rarely - once or twice an episode - or they become noise.
