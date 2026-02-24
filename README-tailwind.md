# mono/color Tailwind Architecture

This is the Tailwind-based documentation build of mono/color.

Source repository: https://github.com/asvvvad1/mono-color

## File Roles

- `index-tailwind.html`: Single-file Tailwind showcase (layout, themes, components, interactivity).
- `README-tailwind.md`: This architecture reference for the Tailwind version.
- `README.md`: Architecture reference for the original mono/color CSS-layered version.

## Layering Model

The Tailwind setup is intentionally split into 4 layers inside `index-tailwind.html`:

1. Tailwind runtime (`cdn.tailwindcss.com`) + minimal config
2. Theme tokens (`body[data-theme="..."]` CSS variables)
3. Base element styling (`h1/h2/h3`, code/pre/dialog, motion primitives)
4. Interaction layer (plain JavaScript functions for showcase behavior)

This keeps the page self-contained while preserving mono/color visual behavior.

## Theme Token Layer

Themes are controlled by `data-theme` on `<body>`:

- `light`
- `dark`
- `monokai`

Each theme defines the same token contract:

- `--fg`: default text
- `--h`: heading text
- `--bg`: page background
- `--b`: border color
- `--p`: primary/reverse surface
- `--def`: default surface
- `--gray`, `--accent`, `--warning`, `--error`, `--success`, `--info`: utility palette

All major styles and utility-like color choices reference these tokens.

## Tailwind Foundation

Tailwind is used for structural composition and responsive behavior:

- layout: container widths, grid/flex blocks, spacing rhythm
- component surfaces: cards, badges, forms, dialogs, buttons
- responsive patterns: desktop/tablet/mobile preview sections
- utility-first composition replacing mono/color class library dependencies

No `mono.min.css`, `color.min.css`, `light.min.css`, or `dark.min.css` files are loaded in this version.

## Behavior Layer

The page includes a plain JS controller set for interactivity:

- theme controls: `toggleTheme()`, `setTheme()`
- dialogs: `openSampleDialog()`, `closeSampleDialog()`
- token and accessibility tooling: `updateTokenInspector()`, `updateContrastAudit()`
- utility actions: `copyText()`, `copyFromElement()`
- responsive and playground tools: `setPreview()`, `applyPlayground()`
- showcase components: `openToast()`, `toggleDropdown()`, `toggleAccordion()`, `switchUiTab()`, `switchSnippetTab()`
- motion behavior: `initRevealObserver()`
- export flow: `generateStarterDownload()`

## Composition Pattern

As with mono/color, UI is composed from small reusable pieces rather than custom per-component CSS files.

Examples:

- button shell: `rounded-[2rem] bg-[var(--p)] px-4 py-2 text-[85%]`
- alert shell: `rounded-[1rem] bg-[var(--error)] p-4 text-[1.4rem]`
- card shell: `rounded-[1rem] border border-[var(--b)] bg-[var(--def)] p-4`

The difference is that composition is now done with Tailwind utilities plus token references.

## Showcase Modules

`index-tailwind.html` includes the base mono/color content plus a Tailwind-specific “Super Showcase”:

- motion showcase
- responsive preview bar
- component playground (radius/padding/shadow/tone controls)
- theme token inspector with copy actions
- Tailwind class recipes
- accessibility panel (contrast + reduced-motion)
- advanced components (tabs, toasts, dropdown, accordion)
- forms lab (stateful inputs)
- snippet tabs (HTML / classes / JS)
- starter exporter (download generated Tailwind starter HTML)

## Theme Switching

Theme switching is runtime-based:

1. `toggleTheme()` cycles light -> dark -> monokai
2. `setTheme(theme)` updates `body.dataset.theme`
3. dependent panels refresh (`updateTokenInspector()`, `updateContrastAudit()`)

No stylesheet swapping is needed.

## Runtime Dependencies

- Tailwind CDN: `https://cdn.tailwindcss.com`
- GitHub buttons enhancement: `https://buttons.github.io/buttons.js` (for Star/Fork widgets only)

## Design Intent

The Tailwind architecture is optimized for:

- one-file portability
- theme-token consistency with mono/color semantics
- richer live demos without introducing a JS framework
- straightforward extension of showcase modules
- preserving the mono/color look while switching to utility-first implementation
