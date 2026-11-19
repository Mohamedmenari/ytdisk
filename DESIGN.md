---
name: YTDISK
description: A broadcast test bench for turning a file into a video and back, byte for byte.
colors:
  paper: "#e9e5db"
  paper-2: "#e1dccf"
  paper-3: "#d7d1c2"
  ink: "#17170f"
  ink-2: "#34332a"
  muted: "#5d5a4c"
  accent: "#ad3018"
  accent-deep: "#932713"
  accent-ink: "#fdf8ec"
  screen: "#0b0b09"
  screen-2: "#141412"
  screen-ink: "#ece7da"
  screen-muted: "#a29c8c"
  screen-black: "#000000"
  white: "#ffffff"
  paper-wash-10: "rgba(255, 255, 255, 0.10)"
  paper-wash-14: "rgba(255, 255, 255, 0.14)"
  paper-wash-16: "rgba(255, 255, 255, 0.16)"
  paper-wash-18: "rgba(255, 255, 255, 0.18)"
  paper-wash-22: "rgba(255, 255, 255, 0.22)"
  scanline: "rgba(0, 0, 0, 0.26)"
  vignette: "rgba(0, 0, 0, 0.34)"
  accent-wash: "rgba(173, 48, 24, 0.05)"
  good: "#2f6b3a"
  bad: "#a32c18"
typography:
  display:
    fontFamily: "Archivo, system-ui, sans-serif"
    fontSize: "clamp(2.7rem, 6.3vw, 5.35rem)"
    fontWeight: 800
    lineHeight: 0.94
    letterSpacing: "-0.045em"
  headline:
    fontFamily: "Archivo, system-ui, sans-serif"
    fontSize: "clamp(1.85rem, 3.4vw, 2.9rem)"
    fontWeight: 700
    lineHeight: 1.02
    letterSpacing: "-0.035em"
  body:
    fontFamily: "Archivo, system-ui, sans-serif"
    fontSize: "16px"
    fontWeight: 400
    lineHeight: 1.55
    letterSpacing: "0em"
  readout:
    fontFamily: "Azeret Mono, ui-monospace, monospace"
    fontSize: "12px"
    fontWeight: 500
    lineHeight: 1.4
    letterSpacing: "0.01em"
  label:
    fontFamily: "Azeret Mono, ui-monospace, monospace"
    fontSize: "11px"
    fontWeight: 400
    lineHeight: 1.4
    letterSpacing: "0.06em"
  footer:
    fontFamily: "Azeret Mono, ui-monospace, monospace"
    fontSize: "12px"
    fontWeight: 400
    lineHeight: 1.5
    letterSpacing: "0.02em"
  arabic:
    fontFamily: "Almarai, Archivo, system-ui, sans-serif"
    fontSize: "16px"
    fontWeight: 400
    lineHeight: 1.75
rounded:
  square: "0"
  tick: "50%"
spacing:
  page: "clamp(20px, 4vw, 44px)"
  xs: "6px"
  sm: "10px"
  md: "18px"
  lg: "28px"
  section: "clamp(46px, 6vw, 78px)"
components:
  button-primary:
    backgroundColor: "{colors.accent}"
    textColor: "{colors.accent-ink}"
    rounded: "{rounded.square}"
    padding: "15px 17px"
  button-primary-hover:
    backgroundColor: "{colors.accent-deep}"
    textColor: "{colors.accent-ink}"
  button-ghost:
    backgroundColor: "transparent"
    textColor: "{colors.ink}"
    rounded: "{rounded.square}"
    padding: "9px 13px"
  segment-active:
    backgroundColor: "{colors.ink}"
    textColor: "{colors.paper}"
    rounded: "{rounded.square}"
    padding: "7px 4px 6px"
  drop-zone:
    backgroundColor: "rgba(255, 255, 255, 0.14)"
    textColor: "{colors.ink}"
    rounded: "{rounded.square}"
    padding: "clamp(26px, 3.6vw, 40px) 18px"
  result-card:
    backgroundColor: "rgba(255, 255, 255, 0.22)"
    textColor: "{colors.ink}"
    rounded: "{rounded.square}"
    padding: "14px"
---

# Design System: YTDISK

## Overview

**Creative North Star: "The Broadcast Bench"**

The page is a public-information test card rebuilt as a physical instrument. A bone-paper desk holds printed rules, numbered procedures, and a dark CRT monitor; one vermillion signal marks the live path. Nothing floats, nothing glows, nothing is rounded. The interface earns trust by looking measured: hairlines, tabular figures, framed readouts, and a single accent that behaves like a tally lamp.

The world borrows from broadcast test patterns, lab benches, and printed service manuals, not from SaaS dashboards. The dark monitor is the only large dark field; the rest is warm paper with ink rules. The file itself is shown as the same high-contrast cell grid the encoder writes, so the product's mechanism is the hero image.

**Key characteristics:**

- Bone paper, near-black ink, one deep vermillion signal.
- Square geometry, 1px rules, 1px column gaps; no cards with radii or shadows.
- Monospace for anything measured; grotesque for anything spoken.
- A dark CRT panel with scanlines and a live timecode.
- Bilingual by construction, with true RTL and bidi-isolated numbers.
- Density is deliberate; functional text never drops below 11px.

## Colors

A warm neutral paper field, ink for structure, and a single oxidized-red signal. The palette is intentionally cream; it is the paper of the bench, not a generic beige landing page.

### Primary

- **Bench Paper** (`#e9e5db`): the page field, with a 22px radial dot grid at 5.5% ink. This is the default surface for reading and for the console.
- **Paper Shadow** (`#e1dccf`): hover fills, inset controls, the quieter side of a two-tone surface.
- **Paper Edge** (`#d7d1c2`): progress tracks and the deepest paper tone.
- **Ink** (`#17170f`): type, 1px structural rules, the console/monitor divider, and the dark full-bleed band.
- **Soft Ink** (`#34332a`): secondary headings and hover ink.
- **Muted Ink** (`#5d5a4c`): captions, labels, helper copy; 5.5:1 on paper.
- **Vermillion Signal** (`#ad3018`): the one accent. Active tab underline, live LED, primary button, step numbers, selected table row marker, focus ring. Chosen at 4.9:1 on paper so body-size accent text passes AA.
- **Deep Vermillion** (`#932713`): pressed/hover state for the primary button; never used as body text.
- **Signal Paper** (`#fdf8ec`): text on vermillion.

### Screen

- **Screen Black** (`#0b0b09`) and **Screen Charcoal** (`#141412`): the CRT body.
- **Screen Ink** (`#ece7da`): readouts on the dark panel.
- **Screen Muted** (`#a29c8c`): monitor labels.
- **Screen Rule** (`rgba(236, 231, 218, 0.16)`): hairlines inside the monitor.

### Status

- **Pass Green** (`#2f6b3a`): result card top rule, check tick, "works" pill, healthy capability LED.
- **Fail Red** (`#a32c18`): failed verification, damaged result card, "fails" pill.

Status is never carried by color alone: every LED has a text label, every pill has a word, every result has a sentence.

## Typography

**Archivo** carries display and interface voice. **Azeret Mono** carries every measured value, label, filename, hash, and timecode. **Almarai** replaces Archivo for Arabic, with looser leading and no negative tracking. All three are self-hosted WOFF2; there are no external font requests.

### Display

- `clamp(2.7rem, 6.3vw, 5.35rem)`, 800 weight, `line-height: 0.94`, `letter-spacing: -0.045em`, `font-stretch: 94%`.
- Hero H1 only. Arabic uses the same clamp but `line-height: 1.14` and `letter-spacing: 0`.
- Section headings use `clamp(1.85rem, 3.4vw, 2.9rem)`, 700, `line-height: 1.02`.

### Body

- 16px / 1.55 Archivo; lede scales to 16–18.5px / 1.6.
- Arabic body: 1.75 leading; paragraphs get the same measure but a little more air.
- Prose measure is capped at 62ch (lede) or 34–48ch (notes and columns). No full-width paragraphs.

### Labels and readouts

- Micro-label floor is **11px**. Mono labels use `0.06em`–`0.12em` tracking, uppercase.
- Measured values use 12px Azeret Mono, tabular numerals, `text-align: end` in ledgers.
- Code is allowed at 10px (code context is exempt); legal smallprint is allowed at 10px.
- No functional label, link, button, table header, or timecode below 11px.

### Bidi

Numbers, hashes, resolutions, timecodes, and Latin technical strings are isolated LTR inside the RTL page (`direction: ltr; unicode-bidi: isolate`). Arabic labels can stay RTL around them. Never let a timecode or a negative number reorder visually.

## Layout

- Page container: `max-width: 1280px`, `padding-inline: clamp(20px, 4vw, 44px)`.
- Hero: two columns, `1.5fr / 0.82fr`, aligned to the top; collapses to one column at 900px.
- Bench: one framed unit with a 1px ink gap between the dark monitor (`1.42fr`) and the paper console (`0.88fr`). It is a single bordered object, not two cards.
- Monitor: flex column; the screen fills the available height on desktop (min 320px), fixed 16:9 below 900px.
- Console: tabs, drop zone, options, ledger, primary action, result. One vertical rhythm, 18px default gap.
- Full-bleed bands: the "how" section and the dark limits section break the container to the viewport edges. This is intentional; their inner content is still inset to the page gutter.
- Chain: four columns with hairline dividers; two columns at 1120px; one column at 640px.
- Table: six columns on desktop; the signal column is hidden below 640px so the remaining five keep their measure.
- Footer: two wrapping groups, page gutter, 11px mono.

### Breakpoints

- **1120px**: hero and bench tighten; chain becomes 2 × 2.
- **900px**: hero, bench, and proof become one column; the capability text hides; the screen returns to 16:9.
- **640px**: brand subtitle hides; hero type tightens; monitor readouts become 2 × 2; table drops the signal column; chain becomes one column.

## Elevation & Depth

The system is flat. Depth is drawn with 1px rules, tonal paper steps, and one 1px gap between the monitor and console. There are no drop shadows on cards, buttons, or panels. The sticky header uses a translucent paper wash and a 10px backdrop blur to separate itself while scrolling; that is the only blur in the paper world.

The dark monitor has a CRT texture: a 1px repeating scanline gradient plus a soft vignette, multiplied over the canvas. This is surface texture, not elevation. There is no glow, no neon, no gradient fill on text.

## Shapes

- Everything is square: buttons, segments, inputs, cards, table cells.
- The only circle is the 17px result tick.
- Hairlines are 1px; emphasis rules are 2px (active tab, progress bar, verify strip) or 3px (result card top).
- The drop zone is a 1px dashed rectangle; drag-over turns it solid vermillion with a 9% red wash.
- The selected proof row is marked by a 5px vermillion square before the label, not a full-height side tab.

## Components

### Header

Sticky, 66px (58px on mobile), paper at 94% opacity with a 1px ink bottom rule. Brand mark is a 26px pixel-grid glyph; the wordmark is Archivo 800 at 108px stretch. The capability readout is a 7px LED plus a mono sentence. The language toggle is a two-cell outlined group; the active cell inverts to ink.

### Hero

H1 in Archivo 800, max 15ch. A 62ch lede below. The right rail is a top-ruled spec strip (three measured facts) and a warning note with a vermillion triangle. On mobile the rail follows the lede and never becomes a card.

### Monitor

Dark charcoal body, 14px padding. Top bar: live LED + "TRANSMISSION", centered resolution, right-aligned timecode. The screen is black with a 1px screen rule, the canvas, a corner tag ("DEMO LOOP" / "RENDERING" / "DECODING" / "COMPLETE" / "NO SIGNAL"), and an optional full-screen note for errors. Four readout cells below: grid, cell, bits/frame, data/frame.

### Tabs

Two equal cells, 1px ink bottom rule, 2px vermillion underline on the active tab. Numbers are mono 11px; labels are Archivo 600 14px. Keyboard: arrows, Home, End.

### Drop zone

Dashed 1px rectangle on a barely lighter paper wash. Center stack: 28px upload glyph, 15.5px semibold prompt, 11px mono hint, 11px mono constraint. Whole label is focusable; Enter/Space opens the picker. Drag-over uses a red wash and a solid red rule.

### Segmented controls

Outlined group, each option a stacked value (12.5px mono) and hint (11px mono uppercase). Active option inverts to ink. Used for cell size, parity, and output resolution. 4K is disabled with an explanation when the encoder cannot handle it.

### Password field

Outlined paper field; focus adds a vermillion 1px ring. Mono input, placeholder `AES-256-GCM · scrypt`. A "show/hide" cell on the inline end, 11px uppercase.

### Ledger and metadata

Top ink rule, dotted separators, label left / value right in mono. Empty values use an em dash. Values are tabular and bidi-isolated. The unpack metadata uses the same rhythm but with 11px mono labels and a truncated hash.

### Primary action

Full-width vermillion rectangle, 15px semibold label, 19px arrow. Hover deepens the red and nudges the arrow 3px; in RTL the arrow is mirrored. Disabled returns to transparent paper with a muted rule and muted text. This is the only large saturated field on the paper side.

### Progress

Framed paper panel with a label + percentage row, a 5px track, and a footer with a detail string and a Cancel link. The bar is vermillion; the percentage is vermillion mono. Cancellation is a text action, not a second button.

### Result card

1px ink frame with a 3px status top rule (green pass, red fail). Head row: 17px circular tick + filename. Sub row: size, duration, resolution, frame count in mono. Actions: solid "Download", ghost "Self-check". The self-check verdict is a 2px left strip with a tinted wash, green or red.

### Proof table

Ink header rule, hairline row rules, mono uppercase 11px headers, 12.5px body. The winning row gets a 5% vermillion wash and a 5px vermillion square before its label. Pills are 1px outlined mono 11px with a 4px square marker. On mobile the signal column is removed; nothing else is hidden.

### Limits band

Full-bleed ink field with paper text. Two columns of four plain statements, separated by 24%-opacity paper hairlines. Headings are paper; body is paper at 72%; bold leads are full paper. No icons, no cards.

## Do's and Don'ts

- **Do** keep the cream paper and the CRT scanlines. The detector may call them "cream palette" and "repeating stripes"; both are the committed world, not an accident.
- **Do** keep functional text at 11px or larger. Code and legal smallprint may sit at 10px. The audit checks this.
- **Do** use the vermillion accent for one job at a time: active state, primary action, or status. Do not flood a section with it.
- **Do** isolate numbers, hashes, and timecodes LTR in Arabic. Check the table, ledger, and monitor at 390px.
- **Do** preserve the 1px ink gap between monitor and console; it is the bench's seam.
- **Do** let full-bleed bands touch the viewport edges; their content still respects the page gutter.
- **Don't** add rounded cards, drop shadows, glassmorphism, gradient text, or a second accent.
- **Don't** shrink labels to fit. Shorten the label or widen the cell instead.
- **Don't** center body copy. Only the drop-zone stack and the fine print are centered.
- **Don't** use color alone for status. Pair every LED and pill with a word.
- **Don't** introduce a CDN, a web font request, or a build step. The page must open from `file://`.
- **Don't** promise recovery past the parity budget. The copy says "repair" only where the decoder can actually repair.
