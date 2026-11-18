# TCG Centering Checker

Measure the centering of trading cards (Pokémon, One Piece, MTG, Lorcana, Yu-Gi-Oh! …) from a photo and see the best centering grade possible at the major graders.

**Live:** https://heroheman.github.io/tcg-centering-checker/

## Features

- Load a photo via file picker, drag & drop or clipboard paste.
- Measure with lines, or with two 4-point segments per axis (averaged, tolerant to slight tilt).
- Fine rotation down to 0.001°.
- Perspective correction from the four card corners (63 × 88 mm or 59 × 86 mm); the original photo is kept.
- Loupe in the corner or at the cursor, zoom 1.5× to 12×.
- Multiple cards with front and back, stored in the browser (nothing is uploaded).
- Grades for PSA, CGC, BGS, SGC, TAG and EDGE, plus AOG centering points.
- A single static HTML file: no build, no server, no dependencies.

## Controls

| Action | Input |
| --- | --- |
| Move line / point | drag; hold <kbd>Alt</kbd> for 10× finer |
| Nudge selected line / point | arrow keys, <kbd>Shift</kbd> for coarse |
| Rotate | <kbd>Q</kbd> / <kbd>E</kbd> ±0.01°, <kbd>Shift</kbd> ±0.1°, <kbd>Alt</kbd> ±0.001° |
| Loupe mode | <kbd>L</kbd> (off, corner, cursor) |
| Loupe zoom | slider or mouse wheel over the image |

## Calculation

Per axis: left share = left border / (left + right border), same for top/bottom. The worse axis determines the grade.

| Grader | Front 10 / 9 / 8 / 7 | Back 10 / 9 / 8 / 7 |
| --- | --- | --- |
| PSA | 55 / 60 / 65 / 70 | 75 / 90 / 90 / 90 |
| CGC | 55 / 60 / 65 / 70 | 75 / 90 / 90 / 90 |
| BGS | 50 / 55 / 60 / 65 | 50 / 70 / 80 / 90 |
| SGC | 55 / 60 / 65 / 70 | 55 / 60 / 65 / 70 |
| TAG | 55 / 60 / 65 / 70 | 65 / 75 / 95 / 99 |
| EDGE | 55 / 60 / 70 / 75 | 70 / 80 / 90 / 90 |

AOG scores centering from 0 to 100: per axis, a 5-point difference between both sides is free, each further point costs one. 50 or less, or 2/3 to 1/3 or worse, counts as off-center (OC). The total weights front 100 % and back 70 %.

Results are guidance, not a guarantee.

Sources: [edgegrading.com](https://edgegrading.com/centering/), [cgccards.com](https://www.cgccards.com/card-grading/grading-scale/), [taggrading.com](https://taggrading.com/pages/scale), [ao-grading.com](https://ao-grading.com/blogs/news/aog-beurteilungs-skala)

## Development

Everything lives in [`index.html`](index.html). Serve it with any static server, e.g. `python3 -m http.server`. Deployed via GitHub Pages from `main`.
