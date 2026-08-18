# Tanmay Lipare — Portfolio

A single-file, cinematic personal portfolio built as a fun side project and
first pass at using React + GSAP together for the web. The hero section's
layout was inspired by the Lando Norris homepage; the overall visual language
(deep red/black on off-white, a spider-web motif, a hanging portrait) is a
loose homage to one of my favorite superheroes, reworked into something that
reads as a developer portfolio rather than a fan page.

## What this is

One `index.html` file. No build step, no `npm install` — React, Tailwind,
GSAP, and Babel are all pulled in via CDN `<script>` tags, and the JSX is
authored directly in an in-browser Babel `<script type="text/babel">` block.
Open the file in a browser and it runs.

That tradeoff is intentional for a project this size, but see
[Known limitations](#known-limitations) before treating this as a template
for anything larger.

## Tech stack

| Piece | Source | Role |
|---|---|---|
| React 18 / ReactDOM | cdnjs (UMD build) | Component structure |
| Babel Standalone | cdnjs | Compiles JSX in the browser at runtime |
| Tailwind CSS | `cdn.tailwindcss.com` | Utility-first styling, custom theme (colors/fonts) via `tailwind.config` |
| GSAP + ScrollTrigger | cdnjs | All motion — entrances, scroll-triggered reveals, ambient loops |
| Google Fonts | Big Shoulders Display, Fraunces, Inter, JetBrains Mono | Display / italic accent / body / mono type |

## Sections

- **Nav** — fixed, blurred header with underline-hover links and a lifted CTA button.
- **Hero** — a cursor-following "punch-hole" reveal between two photo layers
  (a developer photo underneath, a superhero photo masked on top with a
  soft-edged circular hole that follows the mouse), plus a bold three-line
  headline reveal and a quiet breathing-scale ambient loop.
- **About** — a portrait suspended on a thread (`HangingProfile`), dropped in
  and left swinging gently; paragraph and tech-pill reveals sequenced into
  one master `gsap.timeline()`.
- **Work** — a project grid with a restrained hover lift/shadow.
- **Contact** — closing CTA, email link, and social links.

## Motion system

Every animation in the file draws from one small easing vocabulary defined
near the top of the script (`EASE` object), rather than ad hoc curves
scattered around:

- `reveal` (`power4.out`) — decisive text/shape entrances
- `settle` (`expo.out`) — things fading/scaling into frame
- `drop` (`elastic.out(1, 0.6)`) — reserved for objects with implied physical
  weight (the falling corner-webs, the hanging portrait) — the only curve
  allowed to overshoot
- `ambient` (`sine.inOut`) — slow, continuous idle motion
- `hover` (`power2.out`) — fast, no-bounce interactive feedback

Each section's entrance uses `gsap.context()` + `ScrollTrigger`, cleaned up
via `ctx.revert()`; ambient loops (swinging portrait, floating pills, slow
web rotation) are registered through `ctx.add('startAmbient', ...)` and
kicked off together once a section's entrance timeline fully resolves.

## Setup

No install required.

## Credits

- Hero layout/interaction concept inspired by the Lando Norris official
  website.
- Visual theme inspired by a personal favorite superhero — reinterpreted
  through an original, non-branded spider-web motif (geometric SVG, not
  copyrighted artwork) so the design doesn't rely on any licensed IP.
- Built with React, Tailwind CSS, and GSAP/ScrollTrigger.