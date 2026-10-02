# Feature Specification: Intellectual Frontiers design system

**Spec ID:** 0007-design-system · **Constitution:** 1.2.1 · **Status:** Implemented
**Governs:** `design-system/` in this repository and every consumer's vendored copy.

**Input:** One public design system for every Intellectual Frontiers web property, built as Bare
Metal Software (see `context/glossary.md`): strict modern HTML5, modern CSS and modern JavaScript
with web components, no framework, near-zero dependencies.

## Requirements

- **FR-001**: Tokens MUST be CSS custom properties in `css/tokens.css`, mirrored in `tokens.json`.
  Colors, type scale, zero radius and unit colors change only by amending this spec.
- **FR-002**: Styling MUST be modern CSS in cascade layers (`reset, tokens, base, chrome,
  components`), using logical properties, nesting, range media queries and `color-mix()`. No CSS
  framework, no utility classes, no CSS build tool. Class names are semantic.
- **FR-003**: `css/bundle.txt` MUST list the CSS files in cascade order. A consumer concatenates
  them; fonts are referenced relative to `css/`.
- **FR-004**: Fonts (Inter, Source Serif 4, IBM Plex Mono) MUST be self-hosted `woff2`; Inter and
  Source Serif 4 are variable fonts clamped to the weights in use. Consumers SHOULD preload the
  two above-the-fold faces. No third-party font host.
- **FR-005**: Web raster images MUST be WebP in responsive sizes. Brand master PNGs stay for
  non-web use (email signatures, print).
- **FR-006**: The header and breadcrumb band MUST be one sticky unit; anchors clear it through
  `--chrome-clearance`.
- **FR-007**: A page MUST have exactly one breadcrumb `<nav>`. Folding MUST be CSS-only, driven by
  `data-fold-sm`, `data-fold-lg` and `data-tail-lg` set by the server: tail 2 below 48rem, tail 3
  from 48rem (2 when 3 would hide a single crumb); two or more hidden ancestors fold into an
  ellipsis menu. Home has no breadcrumb band.
- **FR-008**: Dropdowns MUST be native popovers placed with CSS anchor positioning, with outside
  click, Escape and link-follow closing and no script. A section with more than three items uses an
  "In this section" menu; otherwise its items render inline from 48rem.
- **FR-009**: The super footer MUST render from `data/navigation.json`.
- **FR-010**: The only script is `js/chrome.js`, which defines the `if-shelf` web component over
  native scroll-snap. `js/datastar.js` is opt-in per page for server-driven interactivity.
- **FR-011**: Interactive widgets MUST be light-DOM web components that degrade to readable,
  usable elements without script, per spec 0008 FR-009 and FR-012.
- **FR-012**: Every component MUST be usable at 375, 768, 1024 and 1440 px wide.
- **FR-013**: A change to this directory MUST be public and MUST be re-vendored by consumers.

## Success criteria
- **SC-001**: A consumer's screenshots of its pages at the four widths match its visual baseline,
  with menus open and the header pinned after scroll.
- **SC-002**: The breadcrumb fold rules of FR-007 hold for trails of 4, 5, 6 and 8 crumbs at 375,
  768 and 1280 px.

## Open questions
- **OQ-1**: Dark theme tokens exist behind `[data-theme="dark"]` and are not wired to a switch.
- **OQ-2**: Only latin font subsets are shipped.
