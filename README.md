# Gumroad — Tipping prototype

An animated HTML/CSS/JS prototype of Gumroad's **"Leave a tip?"** checkout step,
rebuilt from the Figma design (file `YjLc2wyJ9b52NPNEWhlJNJ`, frame `2030:32`).
Single self-contained file — open `index.html` in any browser, no build step.

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

- Cards: hover **lift** with a hard black offset shadow; **press** collapses it
- Selection: gray fill + shadow snap with a subtle **pop**
- Total: **rolls** to the new value when the tip changes
- Custom field: height/opacity **reveal**
- Pay: press + **spinner**, then a slide **transition** to the success screen
- Success: checkmark **badge-in** + **stroke draw**, staggered content, **confetti**
- Respects `prefers-reduced-motion`

Gumroad pink (`#ff90e8`) is used for focus rings and the success flourish; the
core sheet stays monochrome to match the design.

## Responsive behaviour

- **Desktop** — centered sheet/modal on a soft canvas
- **Mobile (≤480px)** — bottom-anchored sheet with a grab handle and slide-up entrance

## Run

```
open index.html          # macOS
# or just double-click the file / serve the folder with any static server
```
