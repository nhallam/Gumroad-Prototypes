# Gumroad — Tipping prototype

An animated HTML/CSS/JS prototype of Gumroad's **"Leave a tip?"** checkout step,
rebuilt from the Figma design (file `YjLc2wyJ9b52NPNEWhlJNJ`, frame `2030:32`).

### Files

| File | What it is |
|---|---|
| `index.html` | **The page** — titled "Gumroad Tipping Prototype"; embeds the prototype and is where more prototypes stack below. |
| `tip.html` | **The prototype** — the self-contained "Leave a tip?" flow (also opens standalone). |

`index.html` embeds `tip.html` in an `<iframe>`, so **serve the folder** to view the
page (e.g. `python3 -m http.server`, then open `/`). Opening `tip.html` directly
in a browser works with no server. To add another prototype, drop a new
`<section class="section">` into `index.html` above the "More coming soon" slot.

## What it is

A faithful reproduction of the tip-selection sheet in Gumroad's neo-brutalist
style (1px black borders, flat white cards, hard offset shadows, bold grotesk
type), made fully interactive and responsive for **desktop and mobile web**.

### Flow / screens

1. **Leave a tip?** — the screen from the Figma frame:
   - 2×2 grid: `20% · US$14.86`, `25% · US$18.58` (pre-selected), `30% · US$22.30`, `Custom`
   - full-width **No tip**
   - live **Total** (default `US$92.92`) and a black **Pay** button
2. **Custom amount** — choosing *Custom* reveals an inline amount field; the Total
   updates live as you type.
3. **Thank you** — after *Pay*, an animated success sheet with a drawn checkmark,
   confetti, and a receipt (Subtotal / Tip / Total paid).

> **Note on scope.** Only frame `2030:32` was available to work from (the Figma
> REST API host is blocked by this environment's network policy, so the rest of
> the connected flow couldn't be pulled). The **tip-selection screen is an exact
> rebuild** of the provided design; the **Custom** and **Thank-you** states are
> reconstructed from what the flow implies. They're isolated in the markup so
> real Figma screens can be dropped in later.

### The numbers

The preset tip amounts (`14.86 / 18.58 / 22.30`) are taken verbatim from the
design. With 25% selected the mock reads `Total US$92.92`, which implies a
**subtotal of US$74.34** — that's the single source of truth in the code, so the
Total stays consistent across every option and custom amount.

## Animations

- Buttons match gumroad.com: **rollover** lifts up-left with a hard black
  shadow; **click** collapses it flat (pressed into the page). The primary
  **Pay** button is black at rest and turns **pink** on hover, like "Start selling".
- Selection: pink wash + shadow snap with a subtle **pop**
- Total: **rolls** to the new value when the tip changes
- Custom field: height/opacity **reveal**
- Pay: press → **spinner**, then a slide **transition** to the success screen
- Success: checkmark **badge-in** + **stroke draw**, staggered content, **confetti**
- Respects `prefers-reduced-motion`

### Brand — aligned to Gumroad's real design system

The tokens are taken from the open-source Gumroad app
([antiwork/gumroad](https://github.com/antiwork/gumroad),
`app/javascript/stylesheets/_definitions.scss` & `_font.scss`):

- **Palette** — `--pink #ff90e8` (accent), plus `--purple #90a8ed`,
  `--green #23a094`, `--orange #ffc900`, `--red #dc341e`, `--yellow #f1f333`;
  `--body-bg #f4f4f0`.
- **Borders** — 1px solid, **radii** 4px / 8px, **hard shadows** `4px 4px 0`
  and `8px 8px 0` (no blur) — Gumroad's neo-brutalist offset look.
- **Type** — Gumroad's brand face is **ABC Favorit** (proprietary), named first
  in the stack; **Hanken Grotesk** is bundled inline as a base64 woff2 as a
  freely-licensed stand-in, so the file stays self-contained/offline-safe.
- **Dark mode** — uses Gumroad's own dark tokens (`--body-bg #242423`, text
  `#dddddd`, surfaces black). The page follows the viewer's OS/theme toggle;
  the hard shadow flips to light, exactly like Gumroad's dark theme.

Pink is used deliberately: a top seam on the sheet, the selected tip (pink wash
+ pink hard shadow + pink subtext), the Pay button's hard shadow, focus rings,
and the success flourish.

## Responsive behaviour

- **Desktop** — centered sheet/modal on a soft canvas
- **Mobile (≤480px)** — bottom-anchored sheet with a grab handle and slide-up entrance

## Run

```
open index.html          # macOS
# or just double-click the file / serve the folder with any static server
```
