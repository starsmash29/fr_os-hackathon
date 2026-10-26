# FR_OS — Brand and design manual

This is the brand reference for FR_OS (Firewall & Router OS) and its
AI-Perimeter layer. The webUI design system that implements it is in
[DESIGN.md](../DESIGN.md); the tokens live in
`src/frfw/webui/static/fros.css`.

The product name is always written **FR_OS**, with the underscore.

## 1. The mark

The logo is an **F+R monogram**: the `F` (firewall) and the `R` (router)
share one stem, and a raven's silhouette sits in the negative space between
them, holding a ring in its beak.

- **The raven (Corvus)** is the raven of Matthias Corvinus and his Black
  Army: a guardian and a tactician.
- **The ring in the beak** stands for the closed chain of trust: keys,
  integrity, nothing let through that was not checked.
- **45° chamfers and heavy stems** keep the letters geometric and solid.

Status: the monogram exists as raster artwork only. Until a flat vector
version is drawn, the webUI keeps its shield icon in the top bar
(DESIGN.md, "Top bar").

### 1.1 Variants

| Variant | Use | Background |
|---|---|---|
| Full colour | webUI, boot splash, slides, video | Dark (`#000000` / `#080C14`) |
| Monochrome, white on black | Terminal, dark screens | `#000000` |
| Monochrome, black on white | Print, documents | `#FFFFFF` |
| Monochrome, transparent | Engraving, stickers | Transparent |

### 1.2 Clear space and minimum size

- Clear space: **0.5X** on every side, where X is the thickness of the
  F's top bar. No text or other graphic enters this zone.
- Symbol alone (favicon, tray): at least **24 × 24 px**.
- Symbol with wordmark: at least **48 px** high.
- WebUI header: **36 px** high, left-aligned.
- Favicon: a simplified monochrome form at 32 × 32 and 16 × 16 px.

### 1.3 Do and don't

Do:
- use only the approved artwork files;
- keep the 0.5X clear space;
- keep at least 4.5:1 contrast between the mark and its background.

Don't:
- separate, stretch or distort the `F` and the `R`;
- crop, change or drop the raven in the negative space;
- remove the ring from the raven's beak;
- add gradients, textures or shadows outside the approved colours;
- rotate the mark.

## 2. Colour

| Token | Hex | Role |
|---|---|---|
| Cyber Cobalt | `#0052FF` | The F letterform, filled controls (buttons, active state) |
| Tech Chrome | `#C0C0C0` | The R letterform and the raven's wing |
| Electric Cyan | `#00E5FF` | The ring; text accents, links, focus, telemetry |
| Obsidian Void | `#080C14` | Page background, terminal background |
| Pure White | `#FFFFFF` | Text on cobalt, monochrome variant |

Supporting UI colours:

| Use | Hex |
|---|---|
| Card / surface | `#0F172A` |
| Main text | `#F8FAFC` |
| Muted text | `#94A3B8` |
| Border | `#1E293B` |
| OK | `#00E676` |
| Warning | `#FFB300` |
| Alert | `#FF3366` |

**Contrast rule.** Cobalt on Obsidian is about 3.9:1, below the 4.5:1 that
body text needs. So cobalt is used as a *fill* (with white text on it,
about 6:1), and cyan is used for *text* accents (about 13:1 on Obsidian).

Print references for the brand colours:

| Colour | RGB | CMYK | Pantone |
|---|---|---|---|
| Cyber Cobalt | 0, 82, 255 | 88, 68, 0, 0 | 2728 C |
| Tech Chrome | 192, 192, 192 | 28, 20, 20, 0 | Cool Gray 5 C |
| Electric Cyan | 0, 229, 255 | 62, 0, 0, 0 | 305 C |
| Obsidian Void | 8, 12, 20 | 85, 75, 60, 90 | Black 6 C |

## 3. Typography

| Family | Role | Weights |
|---|---|---|
| **Orbitron** | Display: the brand name, page titles, big numbers in slides and video | 700, 800, 900 |
| **Inter** | Everything in the UI: body, labels, tables, metrics, docs | 400, 600, 700 |
| **JetBrains Mono** | Code, CLI, rule listings, logs, addresses | 400, 500, 700 |

- Orbitron is for short display text only, never for paragraphs. It has
  no Latin Extended glyphs (no `ő`, `ű`), so Hungarian display text falls
  back to Inter.
- All three are under the SIL Open Font License 1.1 and are vendored in
  `src/frfw/webui/static/fonts/` with their licence files. The webUI loads
  no remote fonts (security-lessons G11).

## 4. In the product

- **Boot splash:** the full-colour mark on black; the ring may pulse softly
  while the system starts.
- **WebUI header:** the mark at 36 px, left-aligned, next to the wordmark
  in Orbitron.
- **Terminal and logs:** JetBrains Mono on Obsidian, cyan for highlights.
