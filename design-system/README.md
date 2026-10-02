# Intellectual Frontiers design system

> **Canonical and public.** Governed by [`spec-kit/specs/0007-design-system`](../spec-kit/specs/0007-design-system/spec.md).
> Consumers vendor a pinned copy of this directory and never edit it. Built as **Bare Metal
> Software**: strict modern HTML5, modern CSS and modern JavaScript with web components, no
> framework, no build tool.

| Path | What it is |
| --- | --- |
| `css/tokens.css` | Custom properties: brand, unit and diagram colors, type, layout, motion. |
| `css/base.css` | Reset, base typography, focus, print. |
| `css/chrome.css` | Page frame, sticky header, breadcrumb band, popover menus, super footer. |
| `css/components.css` | Typography classes, buttons, hero, ruled lists, shelf, update list. |
| `css/fonts.css`, `fonts/` | Self-hosted `woff2` faces. |
| `css/bundle.txt` | Cascade order for concatenation. |
| `logos/`, `logos/web/` | Brand master PNGs and WebP sizes, light and dark. |
| `images/` | Hero and diagram in WebP sizes, favicon, share card. |
| `templating.md` | Reference for the template vocabulary (spec 0010). |
| `data/registry.json` | The `app-*`, `data-app-*` and `if-*` names content may use (spec 0010). |
| `data/navigation.json` | Primary nav, section menus and prefixes, breadcrumb parents, footer. |
| `js/chrome.js` | Defines the `if-shelf` web component. The only script. |
| `js/datastar.js` | Datastar bundle, loaded only by pages that need server-driven interactivity. |
| `tokens.json` | Machine-readable tokens. |
| `chrome.md` | Anatomy and class contract for the chrome. |

Consume: concatenate `css/bundle.txt` in order (rewrite `../fonts/` to wherever fonts are served),
serve `fonts/`, `logos/`, `images/`, `js/`, and render the markup in `chrome.md`.
