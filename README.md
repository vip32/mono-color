# mono/color Style Architecture

This project is set up as a small layered CSS system where each file has one clear job.

Source repository: https://github.com/asvvvad1/mono-color

## File Roles

- `light.min.css`: Light theme design tokens (`:root` CSS variables).
- `dark.min.css`: Dark theme design tokens (`:root` CSS variables).
- `mono.min.css`: Base, color-agnostic primitives (typography, layout shell, forms, buttons, tables, blockquotes).
- `color.min.css`: Optional enhancement layer (color utilities, grid, cards, spacing/alignment/size helpers).
- `index.html`: Full showcase and documentation page that composes classes from the layers above.
- `template.html`: Minimal starter template using the same architecture.

## Layering Model

The system is intentionally split into 3 layers:

1. Theme tokens (`light.min.css` / `dark.min.css`)
2. Structural base (`mono.min.css`)
3. Optional utility+color extension (`color.min.css`)

This keeps the base style usable without color utilities, while still allowing richer UI when `color.min.css` is included.

## Theme Token Layer

`light.min.css` and `dark.min.css` define the same variables:

- `--fg`: body/content foreground text
- `--h`: heading color
- `--bg`: page background
- `--b`: default border color
- `--p`: primary/reverse surface
- `--def`: default surface

All core styles read from these variables, so switching theme is just swapping which token file is active.

## Base Mono Layer (`mono.min.css`)

This layer provides:

- page shell: `.container`, `.content`
- typography defaults: monospace body + sans-serif `h1/h2/h3`
- primitive UI styling for `input`, `textarea`, `select`, `.btn`
- readable code/tables/blockquote defaults
- semantic helpers:
  - `.primary` (reverse surface)
  - `.default` (default surface)

The base remains minimal and mostly semantic, not component-heavy.

## Color/Utility Layer (`color.min.css`)

This layer extends mono with:

- palette tokens: `--accent`, `--info`, `--success`, `--warning`, `--error`, `--gray`
- text/background/border utilities:
  - text: `.accent`, `.info`, `.white`, `.black`, etc.
  - background: `.bg-accent`, `.bg-info`, etc.
  - border: `.b-accent`, `.b-info`, plus `.border` to enable border width/style
- grid primitives:
  - `.row`, `.col`
  - numeric width classes (`.1`, `.2`, `.3`, `.4`, `.5`) for desktop table-like columns
- reusable utility classes:
  - sizing: `.mega`, `.large`, `.small`, `.nano`
  - spacing: `.p`, `.p04`, `.ph`, `.pv`, `.m`, `.mh`, `.mv`, `.m0`
  - layout/alignment: `.inline`, `.w-50`, `.w-100`, `.tacenter`, `.taleft`, `.taright`
  - shape: `.rounded`, `.pill`
  - hero helpers: `.vh-100`, `.vc`
- basic component primitive: `.card`

## Composition Pattern

UI is built by combining tiny classes instead of writing one-off component CSS.

Examples:

- button: `class="btn bg-success white rounded"`
- alert: `class="bg-error white p rounded small"`
- badge: `class="bg-warning black p04 pill small"`

This keeps styles predictable and easy to remix.

## Theme Switching in `index.html`

The page loads both theme files with different `media` values and toggles them with JavaScript:

- active theme: `media=""`
- inactive theme: `media="none"`

`toggleTheme()` swaps those `media` attributes on `#light-theme` and `#dark-theme`.

## Load Order

Use this order so overrides behave correctly:

1. `light.min.css` (or `dark.min.css`) theme tokens
2. other theme file (inactive or media-conditional)
3. `mono.min.css`
4. `color.min.css` (optional)

`mono.min.css` depends on theme variables, and `color.min.css` extends mono classes/utilities.

## Design Intent

The architecture is optimized for:

- very small CSS footprint
- readable defaults
- dual-theme support
- modular adoption (`mono` only, or `mono + color`)
- class-composition workflow instead of custom component CSS per page
