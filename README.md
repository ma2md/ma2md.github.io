# glint — Design System

**glint** is a free, browser-based toolkit for Stardew Valley mod creators. It makes decorative assets for mod description pages, mainly on Nexus Mods. No account is required.

**Products / surfaces**
1. **Scrolls & Banners** — customizable scroll and banner editor with live preview and PNG export.
2. **Emoji** — game emoji gallery with copy, PNG download and animated GIF export.

Both live in one dark-only, responsive web app in English. The brand was originally named "Ateliê do Vale"; it is now **glint**, always lowercase, shown through the `Wordmark` component.

## Sources
Supplied as uploads (not code for this product — mood and pattern references):
- `uploads/a0b44y…jpg` → `assets/bg-snow-village.jpg` — 1920×1080 snowy village road at dusk. Full-page backdrop.
- `uploads/3sjl.gif` → `assets/glints.gif` — 756×443 animated white pixel stars (replaced the earlier static `glints.png`).
- `uploads/theme_ yet.txt` — "yet" Tumblr theme by pouthongwon. Borrowed: 1px borders on everything, small lowercase/uppercase labels, slow 0.8s ease transitions, Solar icon font approach.
- `uploads/Download_ Theme [42]_ Interloper by glenthemes.html` — Interloper Tumblr theme by glenthemes. Borrowed: small-caps label role with +0.025–0.07em tracking, uppercase quiet headings, Geist body / mono code pairing.

- `uploads/assets-and-fonts-for-design/` (second package): Scrollish frames → `assets/scrollish/{standard,menu,text,chat,solarion}/{left,text,right}.png`; sprite sheets → `assets/sprites/`; game fonts → `fonts/`; `implementation-reference/{renderer,gallery,gif}.js` — logic adapted into `ui_kits/web/lib/` (frame sizes, font mapping, tiling, slicing, exclusions, animation pairing, GIF encoder). `winter-background.jpg` and `stars.png` are byte-identical to the backdrop and glint texture already in `assets/`.

No codebase UI, Figma or logo was provided; the interface is authored from the brief.

---

## Content fundamentals
- **Language:** English, concise. Brand name always lowercase "glint"; as a mark, use `<Wordmark>`.
- **Voice:** quiet and practical. Labels name the thing; buttons name the action. No slogans, no taglines, no hero copy, no "Welcome!".
- **Person:** address the user implicitly (imperative): "Pick a frame", "Click an emoji to copy it". Avoid "we".
- **Casing:** sentence case for buttons and body ("Export PNG", "Text colour"). Small labels and tab names are set in UPPERCASE through CSS (`.adv-caps`), written in sentence case in source.
- **Length:** buttons 1–2 words; hints one line, used rarely; toasts 1–4 words ("Copied to clipboard", "PNG saved", "Couldn’t render GIF").
- **Numbers & codes** in mono: `240×64`, `2×`, `:parsnip:`, `32/40`.
- **Emoji:** never as UI. The only "emoji" are the game's pixel sprites, which are content.
- **Examples:** nav "Scrolls & Banners · Emoji"; panel "Scroll editor"; tabs "Frame · Text · Export"; empty state "No emoji match “cow”."

## Visual foundations
- **Mood:** hushed, wintry, nostalgic, slightly dreamlike. Cold palette only: steel blue, misty blue-gray, deep slate, pale silver text. No warm earth tones, neon, gloss or gradients-as-decoration in the UI.
- **Colour:** slate 975–600 grounds; steel 600–200 accent (`--accent` = steel-400, primary button = steel-300); mist for secondary text; silver for primary text. Semantic states are desaturated (`--frost-ok/warn/error`). The pixel-art assets keep their own colours; everything around them stays cold.
- **Backgrounds:** every page sits on `Scenery` — the full-bleed village photo (fixed, `cover`), a slate protection gradient (35% → 18% → 55% top to bottom), the glints texture at 8–20% opacity (screen blend, slow twinkle) and a sparse canvas of falling snow with rare cross-shaped glints. The scenery should stay visible between and through panels. Glints are the animated pixel-star GIF `assets/glints.gif`, tiled at half size (378px), 50% opacity, pixelated; hidden under reduced motion.
- **Surfaces:** very translucent, low-saturation slate-gray (backdrop saturate .7) (`--surface-panel` 42%, `strong` 56%, `clear` 28%) frosted with a 14px backdrop blur (`--blur-frost`), slight dim. The scenery should read softly through every panel.
- **Borders:** 1px hairlines in cool silver at 12/20/36% alpha. Selected = solid steel-300 border.
- **Corners:** mostly square. 2px controls, 3px panels, 0 for preview frames. Never pills.
- **Shadows:** one soft drop (`--shadow-panel`), one for popovers (`--shadow-pop`), plus a 1px white inner top highlight at 5–10% (`--inset-frost`, `--inset-selected`). No glows except the tiny glint.
- **Gradients:** restrained icy-blue / slate / silver, only on interaction surfaces and rare accents. `--grad-primary` (primary buttons, checked boxes), `--grad-selected` (selected buttons, segments, tags, tiles, switch track), `--grad-active-row` (selected FrameSelector row), `--grad-underline` (selected tab / nav link), `--grad-panel-accent` + `--grad-hairline` (Panel `accent`: one per view), `--grad-track` (slider fill). Never on page backgrounds or text.
- **Primary sheen:** on hover the primary gradient drifts (background-position, 800ms), a narrow blurred silver-blue band sweeps diagonally once (`.adv-sheen`, 1100ms), the border brightens and a soft ice glow appears (`--glow-primary`). Press: 1px down, 98.5% scale, slight dim (90ms). The sweep doesn't loop.
- **Text:** near-white for legibility over the scenery — primary silver-50, secondary silver-200, muted silver-300 (summer: warm whites #fbf6f1 / #f0e4d9 / #e2d2c3).
- **Glint motif:** a small 7px white cross (`.adv-glint-mark`) on the corner of primary and selected controls; a white diamond in selected FrameSelector rows and switch knobs. Sparse — at most a few per view.
- **Game fonts** (`--font-game-stardew` "Stardew Valley", `--font-game-cave` "Cave Story", local TTFs in `fonts/`) render text *inside generated assets only*: Stardew Valley for Parchment and Main Menu, Cave Story for Dialogue Box, Chat and Solarion. Never used for UI.
- **Type:** Geist Light (300) for body and titles; Geist 400/500 for controls and caps labels; Geist Mono for values. Display tops out at 28px — no oversized headings. Caps labels 10.5px, +0.16em.
- **Spacing:** 2/4/6/8/12/16/20/24/32/48/64. Controls 28/34/40px tall. Panel padding 20px, gaps 16px between field groups.
- **Layout:** one stacked column, max 600px, centred (Steam-profile / Tumblr-page rhythm). Navigation is the first block of the stack — a compact 40px frosted bar with the wordmark — not a full-width top bar. Panels follow with 14px gaps. Previews are kept narrow (max 340px) and taller than wide.
- **Sparkle banner:** on the editor, directly after the preview window; on the emoji page, the last block of the stack (like a final post), above the credits — a frosted strip filled with the twinkling pixel-star GIF (`SparkleBanner`, `assets/glints.gif`). Both themes.
- **Previews:** `PreviewFrame` — hairline border, 10px inset, silver corner ticks, checker/dark/mist ground, `image-rendering: pixelated`, integer zoom only. Assets are never cropped. Frame choices are text rows (`FrameSelector`), never thumbnails.
- **Motion:** quiet and atmospheric; strongest on interaction. Panels rise 8px and un-blur over 900ms (stagger with `delay`). Previews re-fade (480ms, `transitionKey`) when the frame or sprite changes. Tab/nav underlines grow from the centre (480ms). Animated emotes alternate two frames (default 400ms). Nothing flashes or pulses continuously except the very slow glint twinkle. Slow and soft: `--ease-hush` cubic-bezier(.33,0,.2,1); 140ms fills, 260ms hovers, 800ms panel fade-in and twinkles. Snow falls at 0.12–0.37 px/frame. `prefers-reduced-motion` zeroes all durations, hides the sheen, stops snow (static frame), the twinkle and emote playback by default.
- **Exports stay clean:** sheen, glints, snow, gradients and preview frames are DOM/CSS only. Exported PNG/GIF come from a separate canvas containing just the frame + text or sprite, smoothing off, transparency preserved.
- **Hover:** background lifts by ~8% silver alpha, border to `--border-strong`, text to `--text-strong`. No scale.
- **Press:** darker fill and a 0.5px nudge down.
- **Focus:** 1px silver outline, 2px offset.
- **Imagery:** cold, foggy, low-saturation, dusk light, film-soft. Avoid sunny or warm photography.
- **Avoid:** generic dashboard cards, icon-in-circle tiles, coloured left-border cards, bluish-purple gradients, glossy buttons, large blur, slogans.

## Summer theme (light)
- Opt-in: `<html data-theme="summer">` + `<Scenery season="summer">`. Tokens live in `tokens/theme-summer.css` and override the semantic aliases only, so every component follows.
- **Mood:** golden-hour lakeside, warm and drowsy, same hush as winter. The scene is light; panels are the same low-saturation frosted gray with a slight warm tint (30/40% alpha) with cream text and desaturated copper accents, gold glints. No yellow cream panels.
- **Scenery:** looping `assets/summer/lake.webm` (poster `lake-poster.png`), a soft protection gradient, slow rising pollen (SnowField `rise`) and the bunny sprite sitting bottom-left (both themes). No petals or sparkles in the backdrop. All pixel GIFs render `pixelated`.
- **Reduced motion:** video replaced by its poster, pollen static.
- The winter rule "no warm earthy colours" applies to winter only.

## Iconography
- **Set:** [Lucide](https://lucide.dev) via the `lucide-static` icon font (CDN, imported in `tokens/fonts.css`). Use `<Icon name="download" />` or `<i class="icon-download">`. **Substitution:** the reference "yet" theme used Solar Icons; Lucide was chosen for its thin 1.5 stroke and reliable CDN. No icon files were supplied.
- **Size:** 13–15px next to 11–13px labels. Icons inherit text colour; never tinted with an accent.
- **Usage:** functional only — download, copy, film (GIF), zoom-in/out, rotate-ccw (reset), grid-3x3, x, check, github. No decorative icons, no emoji, no unicode pictographs.
- **Glints** are drawn in CSS/canvas (crosses, diamonds), not icons.
- **Wordmark:** "glint" in Geist 300, +0.06em, lowercase, silver → icy-steel gradient text with a one-shot sheen and a small four-point sparkle top right (`Wordmark` component, `.adv-wm` classes). No other logo exists.

## Index
- `styles.css` — entry; imports only.
- `tokens/` — `theme-summer.css` (light theme), `fonts.css`, `colors.css`, `typography.css`, `spacing.css`, `effects.css`, `base.css` (body, links, scenery/glints classes, reduced motion), `components.css` (state classes used by components).
- `assets/` — `bg-snow-village.jpg`, `glints.gif`, `scrollish/` (5 frame styles), `sprites/` (emojis, EmoteMenu, emotes-frame-1/2).
- `assets/summer/` — `lake.webm`, `lake-poster.png`, `petals.gif`, `sparkle-gold.gif`, `bunny.gif`.
- `fonts/` — `Stardew_Valley.ttf`, `CaveStoryRegular.ttf` (asset text only).
- `guidelines/` — foundation specimen cards (Colors, Type, Spacing, Brand).
- `components/` — React primitives, each with `.jsx`, `.d.ts`, `.prompt.md`, and one card per folder.
- `ui_kits/web/` — click-through app: Scrolls & Banners editor, Emoji gallery.
- `thumbnail.html`, `SKILL.md`.

### Components
- **brand:** Wordmark
- **core:** Button, IconButton, Icon
- **forms:** TextField, Select, Slider, Checkbox, Switch, SegmentedControl, ColorSwatches, FrameSelector
- **surfaces:** Panel, PreviewFrame, Tag, SparkleBanner
- **navigation:** NavBar, Tabs
- **feedback:** Toast, Tooltip
- **atmosphere:** Scenery, SnowField
- **emoji:** EmojiTile

### Intentional additions
No source defined a component inventory; the set above is sized to the two tools. Product-specific ones: `FrameSelector` (text-based frame list), `PreviewFrame` (crisp framed stage), `EmojiTile`, `ColorSwatches`, `Scenery` + `SnowField` (the atmosphere layer), `Icon` (Lucide wrapper).

### UI kits
- `ui_kits/web/index.html` — glint web app.

## Caveats
- Interface fonts are Google Fonts (Geist, Geist Mono) loaded by URL.
- The kit's scroll/sprite logic lives in `ui_kits/web/lib/` (plain JS), not in the component bundle, because it depends on asset paths. Set `window.ADV_ASSET_ROOT` before loading it from another depth.

## Credits
Stardew Valley assets and fonts: ConcernedApe. Fan-made toolkit. Frame assets sourced through Scrollish / kdau (https://www.kdau.com/scrollish/). Cave Story font credited to its original authors. Inclusion does not imply ownership or a new license.
