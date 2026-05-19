# STBAR — TUI / ANSI Reference

For terminal UIs and Tauri terminal panes. The web CSS lives in `doom.css`;
this document gives you the same look in pure terminal output (ANSI escapes,
box-drawing, block art).

## 1. Color palette — ANSI 256 + truecolor

| Token | Hex (truecolor) | ANSI 256 | Notes |
|---|---|---|---|
| `void` | `#0a0a0a` | `232` | main background |
| `stone` | `#1a1715` | `234` | secondary surface |
| `iron` | `#2a2522` | `236` | panel base |
| `grate` | `#15110e` | `233` | inset cavity |
| `panel-light` | `#7a5e3c` | `137` | bevel highlight |
| `panel` | `#4a3a2a` | `94` | HUD plate |
| `panel-dark` | `#251a10` | `52` | bevel shadow |
| `bone` | `#e8dcc4` | `230` | primary text |
| `bone-dim` | `#b8a886` | `144` | secondary text |
| `ash` | `#6e655a` | `102` | muted / disabled |
| `blood` | `#b51d0e` | `124` | primary red |
| `blood-bright` | `#e8341a` | `196` | hit / alert |
| `hellfire` | `#f96e1f` | `202` | flare / accent |
| `flare` | `#ffb347` | `215` | bright accent |
| `marine-green` | `#36a330` | `34` | health, OK |
| `armor-blue` | `#1e5fb8` | `25` | armor, info |
| `key-yellow` | `#f0c20c` | `220` | warning, key |
| `key-red` | `#d61b1b` | `160` | red keycard |
| `key-blue` | `#1c7be5` | `33` | blue keycard |
| `toxic` | `#7ad932` | `112` | nukage, console |
| `rust` | `#8b4513` | `94` | rust accent |

### Bash quick-reference

```bash
# 256-color foreground:   \e[38;5;<n>m
# 256-color background:   \e[48;5;<n>m
# Truecolor foreground:   \e[38;2;<r>;<g>;<b>m
# Reset:                  \e[0m

# Blood-red text on void background:
printf '\e[38;5;124m\e[48;5;232mRIP AND TEAR\e[0m\n'

# Bone text with hellfire accent:
printf '\e[38;5;230mHealth: \e[38;5;34m100%%\e[0m\n'
```

## 2. Box-drawing — panels, bevels, status bars

The bevel can't be reproduced precisely in a terminal, but you can fake it with
mixed border weights (heavy on bottom/right, light on top/left, or vice versa).

### Light panel — default body content

```
┌──────────────────────────────────────────┐
│ HEALTH                              100% │
│ ARMOR                                75% │
└──────────────────────────────────────────┘
```

### Heavy panel — emphasized / HUD-style

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ THREAT SCANNER                           ┃
┃ Contacts: 3                              ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

### Iron plate — double-line / chrome

```
╔══════════════════════════════════════════╗
║ ► UAC TACTICAL TERMINAL                  ║
║ ► PHOBOS · E1M3                          ║
╚══════════════════════════════════════════╝
```

### Faked bevel — mixed weights for the DOOM panel look

```
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ ARMORY ║                                 ┃
┠─────────╨─────────────────────────────────┨
┃ SHOTGUN          shells       12         ┃
┃ CHAINGUN         bullets      200        ┃
┃ ROCKET LAUNCHER  rockets      14         ┃
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
```

Top + left in heavy weight, bottom + right could also use heavy weight but with
a different "light shadow" character (`░` or `▒`) trailing it to suggest depth.

## 3. Texture & bars — block characters

```
Full block       █  U+2588    health bar fill
Dark shade       ▓  U+2593    armor / metal texture
Medium shade     ▒  U+2592    stone surface
Light shade      ░  U+2591    fog / atmosphere
Quadrants        ▀▄▌▐ ▖▗▘▝▙▟  pixel-precision blips
```

### HUD bars

```
HEALTH  ▐██████████████████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  76%
ARMOR   ▐██████████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  42%
AMMO    ▐██████████████████████████████░░░░░░░░░░░░░░░░░░░  88%
```

Color the fill in marine-green (`34`), armor-blue (`25`), or key-yellow (`220`).
When health drops below 25%, swap the fill to blood-bright (`196`) and flash.

## 4. Status bar template

```
┏━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━┳━━━━━━━━━━┓
┃  HEALTH  ┃  ARMOR   ┃  SHELLS  ┃ BULLETS  ┃ ROCKETS  ┃  THREAT  ┃
┃   76%    ┃   42%    ┃    12    ┃   200    ┃    14    ┃    !!    ┃
┗━━━━━━━━━━┻━━━━━━━━━━┻━━━━━━━━━━┻━━━━━━━━━━┻━━━━━━━━━━┻━━━━━━━━━━┛
```

Colors per cell:
- Health → marine-green `34`
- Armor → armor-blue `25`
- Ammo (shells/bullets/rockets) → key-yellow `220`
- Threat → blood-bright `196` (flashing)

## 5. ASCII DOOM logo

For terminal banners. Set foreground to blood (`124`) with bone background, or
inverse it for the inset-stone look.

```
 ████▄    ▄████▄    ▄████▄    █▄    ▄█
 ▀▀ ███  ███▀▀███  ███▀▀███   ███  ███
 ▄▄ ███  ███  ███  ███  ███   ██████
 ████▀    ▀████▀    ▀████▀    █▀  ▀█
```

A simpler one-line variant:

```
█▀▄ █▀█ █▀█ █▀▄▀█
█▄▀ █▄█ █▄█ █ ▀ █
```

## 6. Voice / patterns for terminal output

- **Prompts** — `▶` or `>` in bone, command in toxic-green.
- **Timestamps** — wrap in `[HH:MM:SS]`, color in ash.
- **OK lines** — prefix `[ OK ]` in marine-green.
- **Warnings** — prefix `[WARN]` in key-yellow.
- **Errors / alerts** — prefix `[!!]` or `[CRIT]` in blood-bright, optionally with `\e[5m` blink (sparingly, many terminals respect it).
- **Headings** — uppercase, surrounded by `═══` rules.

### Sample log block

```
[14:22:08] UAC-NET: Connection established
[14:22:09] Loading marine profile: DOOMGUY
[14:21:51] [!!] Containment field collapsed — sub-level 3
[14:21:32]       Marine team Bravo: last ping 8 min ago
[14:21:14] [CRIT] Gateway flux: CRITICAL
[14:20:11] [ OK ] All systems nominal
```

## 7. Library quick-reference

### Rust — `ratatui`

```rust
use ratatui::style::{Color, Modifier, Style};

const DOOM_BLOOD:     Color = Color::Rgb(0xb5, 0x1d, 0x0e);
const DOOM_HELLFIRE:  Color = Color::Rgb(0xf9, 0x6e, 0x1f);
const DOOM_MARINE:    Color = Color::Rgb(0x36, 0xa3, 0x30);
const DOOM_BONE:      Color = Color::Rgb(0xe8, 0xdc, 0xc4);
const DOOM_PANEL:     Color = Color::Rgb(0x4a, 0x3a, 0x2a);
const DOOM_PANEL_LT:  Color = Color::Rgb(0x7a, 0x5e, 0x3c);
const DOOM_VOID:      Color = Color::Rgb(0x0a, 0x0a, 0x0a);

let title = Style::default()
    .fg(DOOM_BLOOD)
    .add_modifier(Modifier::BOLD);

let panel = Block::default()
    .borders(Borders::ALL)
    .border_style(Style::default().fg(DOOM_PANEL_LT))
    .style(Style::default().bg(DOOM_PANEL).fg(DOOM_BONE));
```

### Python — `rich` / `textual`

```python
from rich.style import Style
from rich.theme import Theme

DOOM_THEME = Theme({
    "blood":     "#b51d0e",
    "hellfire":  "#f96e1f",
    "marine":    "#36a330",
    "armor":     "#1e5fb8",
    "yellow":    "#f0c20c",
    "toxic":     "#7ad932",
    "bone":      "#e8dcc4",
    "ash":       "#6e655a",
    "panel":     "#4a3a2a",
    "panel_lt":  "#7a5e3c",
    "void":      "#0a0a0a",
    # semantic
    "alert":   "bold #e8341a",
    "ok":      "#36a330",
    "warn":    "#f0c20c",
    "ts":      "#6e655a",
})
```

### Go — `bubbletea` / `lipgloss`

```go
import "github.com/charmbracelet/lipgloss"

var (
    Blood    = lipgloss.Color("#b51d0e")
    Hellfire = lipgloss.Color("#f96e1f")
    Marine   = lipgloss.Color("#36a330")
    Bone     = lipgloss.Color("#e8dcc4")
    Panel    = lipgloss.Color("#4a3a2a")
    PanelLt  = lipgloss.Color("#7a5e3c")
    Void     = lipgloss.Color("#0a0a0a")
)

var panelStyle = lipgloss.NewStyle().
    Background(Panel).
    Foreground(Bone).
    BorderStyle(lipgloss.ThickBorder()).
    BorderForeground(PanelLt).
    Padding(1, 2)
```

## 8. Do / don't

- **Do** keep the palette small per screen — bone text on void/iron, blood for alerts, marine-green for healthy state. Hellfire is the accent, not a default.
- **Do** lean on uppercase + wide spacing (`letter-spacing` doesn't exist in TUI, but `M A R I N E` works) for HUD labels.
- **Don't** use truecolor without a 256-color fallback — older terminals (Windows cmd pre-Win10, ttys, dumb pipes) will mangle the escape codes.
- **Don't** mix DOOM with cute emoji or rounded box-drawing variants (`╭╮╰╯`). The world is industrial, infernal, and orthogonal.
