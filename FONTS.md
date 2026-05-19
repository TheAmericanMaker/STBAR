# Fonts

The DOOM look depends on a stack of typefaces. Here's what each one does
and where it comes from.

## Bundled in this repo

### AmazDooM — by Amazingmax

The headline face. AmazDooM is a fan-made recreation of the lettering used
in the original DOOM logo, created by **Amazingmax**. It ships in six
faces (Left, Left2, LeftOutline, Right, Right2, RightOutline). Alternate
Left and Right between adjacent letters to reproduce the dimensional,
"cut into stone" look of the original logo.

- **License:** Free — permitted for personal and commercial use, per the
  listing at [fontmeme.com/fonts/amazdoom-font](https://fontmeme.com/fonts/amazdoom-font/).
- **Designer:** Amazingmax
- **Source:** <https://fontmeme.com/fonts/amazdoom-font/>
- **Files in this repo:** `amazdoom/AmazDooMLeft.ttf`, `AmazDooMLeft2.ttf`,
  `AmazDooMLeftOutline.ttf`, `AmazDooMRight.ttf`, `AmazDooMRight2.ttf`,
  `AmazDooMRightOutline.ttf`

**Huge thanks to Amazingmax** for creating this font and releasing it
freely. If you use this design system in something you publish — a
project, a site, an app — please pass along the credit.

A note on transparency: the TTF metadata embedded in the font files
contains a copyright string referencing ParaGraph (a commercial font
foundry from the 1990s), suggesting AmazDooM may be derived from an
earlier font. The license tag on fontmeme is the authoritative source we're
relying on, but if you're using this in a high-stakes commercial product
and chain-of-title matters to you, contact Amazingmax directly or consult
a lawyer.

## Loaded from Google Fonts (no setup needed)

All loaded via the `<link>` tag in `style-guide.html` and `demo.html`.
All distributed under the SIL Open Font License (OFL) — free for personal
and commercial use, no attribution required (but always welcome).

| Face | Role |
|---|---|
| Black Ops One | Display fallback if AmazDooM is removed |
| Rubik Mono One | Secondary display fallback |
| VT323 | UI labels (HUD, buttons, table headers) |
| Press Start 2P | HUD numeric readouts |
| Special Elite | In-world notes / mission briefings |
| IBM Plex Mono | Body copy across the whole system |

## Fallback behavior

The CSS variables are stacked so that if AmazDooM is missing for any
reason, the next-best face takes over:

```css
--doom-font-display:     'AmazDooMLeft', 'Black Ops One', 'Rubik Mono One', Impact, sans-serif;
--doom-font-display-alt: 'AmazDooMRight', 'Black Ops One', Impact, sans-serif;
```

Black Ops One is a heavy military-stencil display face under OFL that
captures roughly 80% of the DOOM-logo vibe. The system looks good either
way; AmazDooM just nails the *exact* alternating-bevel logo look from 1993.

## If you replace the font

Want a different headline face? Edit `--doom-font-display` in `doom.css`
and update the `@font-face` block at the top. Everything else (HUD,
buttons, body text) will stay in place — the display face is the only
piece tied to AmazDooM.

---

*Nothing in this document is legal advice. License details are reproduced
in good faith from the source linked above; verify the current license
yourself before using in any high-stakes commercial context.*
