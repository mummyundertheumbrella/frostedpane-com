# Task: implement the "Frosted Pane Press" landing page

Read `README.md` in this folder first — it is the complete spec.

You are implementing a single static "coming soon" landing page for **Frosted Pane Press**. It shows the division logo, the headline "Unwrapping 2027", a short subhead, and a contact email. No forms, no navigation, no JavaScript required.

This page is one of six sibling sites across the group. They share one design; only the tint color, logo, division name, and contact email differ. **This repo is Frosted Pane Press only** — do not build the other five here.

## This site's values
| Value | |
|---|---|
| Division name | Frosted Pane Press |
| Tint color | `#7A2010` |
| Logo | `design_handoff/assets/frosted-pane-press.png` |
| Contact email | contact@frostedpane.com |

## Steps
1. Read `README.md` fully — exact hexes, type scale, spacing, and copy are there.
2. Open `design_handoff/reference.dc.html` — the design reference for the page. Compare against `design_handoff/screenshot.png` to see the intended result.
3. Inspect this repo and decide how to implement: existing components, styling approach (CSS modules / Tailwind / styled-components / plain CSS), font loading, asset pipeline. Follow what the repo already does. If the repo is empty, a static setup is appropriate.
4. Move the two images from `design_handoff/assets/` into wherever this repo serves static assets from.

## Rules
- Do NOT port `support.js` or the `<x-dc>` / `<dc-import>` runtime — it is a prototyping tool, not part of the design.
- Keep the `mix-blend-mode: multiply` background treatment. It is load-bearing: the artwork is black linework on cream, and the multiply is what turns the cream into `#7A2010` while keeping the lines black. An opacity overlay is not an acceptable substitute.
- Keep all `clamp()` type sizes fluid rather than freezing to fixed values.
- Copy is final, reproduce verbatim: headline "Unwrapping" / "2027" (explicit line break between them), subhead "Still under wraps. See you next year.", eyebrow "Frosted Pane Press".
- Even though this is one page, build it as a component with the four values above as props or config. The other five sites use the same design, so the seam should be there.
- Add a ~150ms transition on the contact pill's `border-color` and `background` hover change. This is the one intentional addition to the prototype.

## Verify
Renders correctly at desktop and mobile widths; `#7A2010` reads correctly through the artwork; cream text stays legible over the linework; the logo scales without overflow; the mailto link opens to contact@frostedpane.com.
