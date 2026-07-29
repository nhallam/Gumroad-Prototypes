# Gumroad — Tipping prototype

An animated HTML/CSS/JS prototype of Gumroad's **"Leave a tip?"** checkout step,
rebuilt from the Figma design (file `YjLc2wyJ9b52NPNEWhlJNJ`, frame `2030:32`).

### Files

| File | What it is |
|---|---|
| `index.html` | **The page** — titled "Gumroad Tipping Prototype"; embeds the prototypes and is where more stack below. |
| `tip.html` | **Concept 01** — the self-contained "Leave a tip?" bottom-sheet flow (also opens standalone). |
| `checkout.html` | **Concept 02** — tipping built into a full two-column checkout page (also opens standalone). |
| `upsell.html` | **Concept 03** — a pink "Leave a tip?" upsell panel shown on Pay (also opens standalone). |
| `thankyou.html` | **Concept 04** — the thank-you moment: tip on the post-purchase download page (also opens standalone). |
| `backcreator.html` | **Concept 05** — back the creator: goal progress, supporters and a perk (also opens standalone). |
| `slider.html` | **Concept 06** — one fair-price slider that merges price and tip (also opens standalone). |

**Concept 02 — checkout tipping.** A tip module embedded in the order summary with a
type switcher: **Percentage** (preset grid), **Custom** ($ input with "N people left a
tip" social proof), **Round Up** (rounds the order up to the nearest $10), and
**Let's have fun** — a **Coin Catch** mini-game (← → move a basket to catch falling
coins over 12s; each coin is US$0.10, gold ones US$0.30; your score becomes the tip).
Neutral grey marks the active mode/method;
pink marks the chosen tip. The payment column is visual scaffolding (non-functional).

**Concept 03 — tip upsell.** The right column shows the payment form; clicking **Pay**
swaps it for a bold **pink "Leave a tip?" panel** with a **$ Amount / % Percentage**
toggle and presets ($0.25 / $0.5 / $1 / $2 / $5, or 5–25%) + **No tip**. Picking one
updates the Total (in the panel and the order summary); Pay completes to a thank-you.
The left column adds a **"Give as a gift"** toggle. Payment is scaffolding.

**Concept 04 — the thank-you moment.** The tip ask moves *after* the sale: on the
post-purchase download page, once the buyer already has what they paid for, a
gratitude-framed card invites a tip ($1 / $2 / $5 / Custom) with an optional note.
Sending swaps the card for a "💛 Sent" confirmation and a mock reply from the creator —
no pressure at checkout, gratitude instead of an upsell.

**Concept 05 — back the creator.** Reframes the tip as *backing a goal*. A progress bar
shows how close the creator is to a funding goal, with supporter avatars and a live
count; picking an amount previews the bar moving, bumps the supporter count, and reveals
a matching perk (thank-you note → credits → early access). Paying adds you as the next
supporter ("You're supporter #37").

**Concept 06 — one fair-price slider.** Merges price *and* tip into a single
"pay what feels fair" slider anchored at the base price (US$1.08), with a "most people
pay US$3" marker and preset chips (Base only / Fair / Generous / Champion). The creator's
avatar reacts as you drag (🙂 → 😊 → 😍 → 🤩) and the breakdown shows "Base + US$X tip"
live. Fully keyboard-accessible (native range input).

`index.html` embeds the prototypes in `<iframe>`s, so **serve the folder** to view the
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
   - social proof: three overlapping avatars (real Unsplash photos, with an
     illustrated-SVG fallback where external images are blocked) + "12 other people left tips"
   - live **Total** (default `US$92.92`, with the tip amount shown beside it)
     and a black **Pay** button
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
- Selection: solid **brand pink** with a black hard shadow + a subtle **pop**
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
