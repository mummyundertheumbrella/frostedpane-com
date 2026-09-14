# Handoff: Frosted Pane Press — "Unwrapping 2027" Landing Page

## This repo
This handoff covers **Frosted Pane Press** only: tint `#7A2010`, logo `assets/frosted-pane-press.png`, contact contact@frostedpane.com. The six-division table further down is included for context — the design is shared across six sibling sites in six separate repositories — but **only the Frosted Pane Press row applies here.**

See `CLAUDE_CODE_PROMPT.md` for the task, `reference.dc.html` for the design, `screenshot.png` for the intended result.

## Overview
Six near-identical "coming soon" landing pages, one per division of the parent group. Each page shows the division's logo, the shared headline "Unwrapping 2027", a short playful subhead, and a contact email. The only per-page differences are: tint color, logo file, division name, and contact email.

Divisions: Frosted Pane Press, Honey Resin Studios, Olivine Moon Films, MotMot Photography, Hipp Indigo Music, Fuchsia and Fern.

## About the Design Files
The files in this bundle are **design references created in HTML** — prototypes showing intended look and behavior, not production code to copy directly. The task is to **recreate these designs in the target codebase's existing environment** (React, Next.js, Astro, Vue, static site generator, etc.) using its established patterns, component conventions, and styling approach. If no environment exists yet, choose an appropriate framework — these are static pages with no interactivity beyond a mailto link, so a static site generator or plain HTML/CSS build is entirely sufficient.

The `.dc.html` files use a custom prototyping runtime (`support.js`, `<x-dc>`, `<dc-import>`). **Do not port that runtime.** Treat `Division Landing.dc.html` as the single component definition and the six per-division files as its six sets of props.

## Fidelity
**High-fidelity.** Colors, typography, spacing, and layout are final. Recreate pixel-faithfully using the codebase's existing libraries and patterns. All type sizes are fluid (`clamp()`) — preserve the fluid behavior rather than freezing to one breakpoint's values.

## Screens / Views

### Division Landing (one instance per division)

**Purpose:** Announce that the division's site is coming in 2027 and offer a contact email for enquiries. No email capture, no navigation, no countdown.

**Layout**

Root: full-viewport section, `min-height: 100vh`, `width: 100%`, `overflow: hidden`, `box-sizing: border-box`. Background color = the division tint. Flex, `align-items: center`, `justify-content: center`. Padding `clamp(28px, 6vw, 96px)`.

Two absolutely positioned overlay layers fill the root (`position: absolute; inset: 0; pointer-events: none`), in this order:
1. **Background artwork.** `assets/background.png`, `background-size: cover`, `background-position: center`, **`mix-blend-mode: multiply`**. The multiply blend is what makes the tint work: the artwork is black linework on cream, so multiplying over the solid tint keeps the black lines black and turns the cream areas into the tint color. Do not swap this for an opacity overlay — the result is muddy.
2. **Vignette.** `radial-gradient(120% 90% at 30% 50%, rgba(0,0,0,0) 35%, rgba(0,0,0,0.45) 100%)`. Darkens the edges so the cream text holds contrast against the busy linework.

Content wrapper (above the overlays, `position: relative`): `width: 100%`, `max-width: 1180px`, flex row, `flex-wrap: wrap`, `align-items: center`, `gap: clamp(28px, 5vw, 80px)`.

- **Left column** — `flex: 1 1 260px`, `min-width: 0`, flex with `justify-content: center`. Holds the logo image: `width: 100%`, `max-width: 420px`, `height: auto`, `display: block`, `filter: drop-shadow(0 18px 40px rgba(0,0,0,0.45))`.
- **Right column** — `flex: 1 1 340px`, `min-width: 0`, flex column, `align-items: flex-start`, `gap: clamp(18px, 2.4vw, 30px)`.

Because both columns use `flex-wrap` with flex-basis floors of 260px and 340px, the layout collapses to a single stacked column (logo above text) below roughly 700px of available width. That is the intended mobile behavior.

**Components (right column, top to bottom)**

1. **Division eyebrow** — the division name. Karla 500, `font-size: clamp(11px, 1.1vw, 14px)`, `letter-spacing: 0.34em`, `text-transform: uppercase`, color `rgba(255,248,236,0.78)`.
2. **Headline** — `h1`, text "Unwrapping" / line break / "2027". Eczar 700, `font-size: clamp(44px, 8.2vw, 108px)`, `line-height: 0.94`, `letter-spacing: -0.01em`, color `#FFF6E8`, `text-wrap: balance`, `margin: 0`. The line break is explicit, not a wrap.
3. **Rule** — `width: clamp(64px, 12vw, 140px)`, `height: 2px`, background `rgba(255,246,232,0.45)`.
4. **Subhead** — exact copy: "Still under wraps. See you next year." Karla 400, `font-size: clamp(15px, 1.5vw, 19px)`, `line-height: 1.55`, color `rgba(255,246,232,0.86)`, `max-width: 34ch`, `text-wrap: pretty`, `margin: 0`.
5. **Contact pill** — an `<a href="mailto:…">` whose visible label is the email address itself. `display: inline-flex`, `align-items: center`, `gap: 10px`, `margin-top: 4px`, `padding: 14px 22px`, `border: 1.5px solid rgba(255,246,232,0.5)`, `border-radius: 999px`, `font-size: clamp(14px, 1.3vw, 16px)`, `letter-spacing: 0.02em`, color `#FFF6E8`, `text-decoration: none`.
   **Hover:** `border-color: #FFF6E8`; `background: rgba(255,246,232,0.1)`. Add a `transition` of ~150ms on `border-color, background` in the port (the prototype has none).

## Interactions & Behavior
- Contact pill opens the user's mail client via `mailto:`. Nothing else is clickable.
- No motion or entrance animation — deliberate, per the brief.
- Only the pill hover state above.
- No loading, error, or form states. No JS required.
- Responsive: fluid type throughout; single-column stack below ~700px as described.

## State Management
None. These are static pages. The four per-division values are build-time props/config, not runtime state:

| Prop | Type | Notes |
|---|---|---|
| `tint` | string (hex) | Root background color |
| `logo` | string (path) | Logo image src |
| `division` | string | Eyebrow text |
| `email` | string | Pill label **and** mailto target |

## Design Tokens

**Division tints** (root background, one per site)

| Division | Tint | Logo | Email |
|---|---|---|---|
| Frosted Pane Press | `#7A2010` | `frosted-pane-press.png` | contact@frostedpane.com |
| Honey Resin Studios | `#7A5015` | `honey-resin-studios.png` | contact@honeyresin.com |
| Olivine Moon Films | `#2E4A10` | `olivine-moon-films.png` | contact@olivinemoon.com |
| MotMot Photography | `#1A4848` | `motmot-photography.png` | contact@motmoteye.com |
| Hipp Indigo Music | `#2A2868` | `hipp-indigo-music.png` | contact@hippindigo.com |
| Fuchsia and Fern | `#701A62` | `fuchsia-and-fern.png` | contact@fuchsiaandfern.com |

**Ink**
- `#FFF6E8` — headline, pill label and border-hover
- `rgba(255,248,236,0.78)` — eyebrow
- `rgba(255,246,232,0.86)` — subhead
- `rgba(255,246,232,0.45)` — rule
- `rgba(255,246,232,0.5)` — pill border
- `rgba(255,246,232,0.1)` — pill hover fill
- `#14100c` — html/body background behind everything

**Typography**
- Display: **Eczar** 700 (Google Fonts) — headline only. Fallback `Georgia, serif`.
- Text: **Karla** 400/500 (Google Fonts) — everything else. Fallback `system-ui, sans-serif`.
- Scale: headline `clamp(44px, 8.2vw, 108px)` / 0.94; subhead `clamp(15px, 1.5vw, 19px)` / 1.55; pill `clamp(14px, 1.3vw, 16px)`; eyebrow `clamp(11px, 1.1vw, 14px)`, tracking 0.34em.
- Import: `https://fonts.googleapis.com/css2?family=Eczar:wght@500;700&family=Karla:wght@400;500&display=swap` (self-host in production if the codebase does that).

**Spacing**
- Page padding `clamp(28px, 6vw, 96px)`; column gap `clamp(28px, 5vw, 80px)`; right-column stack gap `clamp(18px, 2.4vw, 30px)`.

**Radius / shadow**
- Pill radius `999px`. Logo `drop-shadow(0 18px 40px rgba(0,0,0,0.45))`. No other radii or shadows.

## Assets
All supplied by the client and included in `assets/`:
- `background.png` — shared mummy-wrap linework artwork, black on cream. Used on all six pages under `mix-blend-mode: multiply`. Do not recolor the file itself; the tint comes from the blend.
- Six logo PNGs, one per division, named in the table above.

Logos are raster PNGs. If vector originals (SVG) exist, prefer them — the logos render up to 420px wide and scale with the viewport.

## Files
Design references in this bundle:
- `CLAUDE_CODE_PROMPT.md` — the task. Start here.
- `reference.dc.html` — the design reference for this page, with Frosted Pane Press's values already applied.
- `screenshot.png` — the intended result, for visual comparison.
- `support.js` — prototyping runtime. Reference only; do not port.
- `assets/background.png` — shared linework artwork.
- `assets/frosted-pane-press.png` — this division's logo.

## Suggested implementation
Build the page as one component taking the four props, with Frosted Pane Press's values supplied from a single config object or constant. The other five divisions ship from their own repositories using the same design, so keeping the values in one place makes this repo easy to diff against its siblings.
