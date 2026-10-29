---
name: anim-world
description: Making the world feel alive and visually cohesive - set life, light and colour, atmosphere, depth, weather and how the cast sits in the painted sets. Use when scenes feel static, the cast looks pasted on, or colours don't match between scenes.
---
# The world, light and colour

## The cast must belong in the painting
- The set's light shades the cast (cel light direction from `light_from`, rim light at night/sunset, cast tint from `PLATE_SETS[...]["cast"]`, lamps warming nearby characters, haze on characters further back). New sets need these values set, or the cast looks pasted on.
- Contact: ground shadows under standing characters (long at sunset), cushion dips under sitters, footprints in sand, dust puffs on landings.
- Scale and depth: spots further back are smaller and hazier; keep the cast's feet on the painting's ground line.

## Alive, not busy
- Every set has `life` in its JSON: birds, leaves, clouds, ripples, townsfolk, bikes, stars, fireflies, fog, flicker, heat haze, puddles. Ambient motion should be slow and small, never pulling focus from faces.
- Depth layers (skill `set-tools`) make camera moves feel like real space; moving parts (doors, trees, curtains, lamps) add life where the story touches them.
- Weather is acting: a storm darkens, flashes, shakes held props, pushes ears and tails, flickers lamps.

## Colour
- Colour script: decide each episode's emotional colour (warm summer, cool tense, faded memory) with `grade:`; the auto colour match keeps sets in the same light consistent across cuts.
- Tense beats sit cooler (automatic); quiet lines desaturate a little; long sunset scenes deepen toward dusk; silhouettes (`[silhouette]`) for big emotional sunset moments.
- Value contrast directs the eye: the face should be the brightest/most contrasted area in its shot.
- Film grain (`grain: on`) unifies painted sets and code-drawn cast; keep it subtle.

## Consistency checks
- Same place, same time of day: same light and grade across beats.
- Time jumps fade through black (automatic on a time-of-day change in the script).
- Night faces must stay readable (cast light capped with act).
