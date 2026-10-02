# Feature Specification: Content format

**Spec ID:** 0008-content-format · **Constitution:** 1.2.1 · **Status:** Implemented
**Governs:** every Intellectual Frontiers web property's content, public or private.

**Input:** Content is strict, modern, semantic HTML5, typed by the ontology, with no front matter
and no second markup language. Built as Bare Metal Software: the standard parser, our own
checks, and the platform for everything else.

## Requirements

### Format
- **FR-001**: A content file MUST be a complete HTML5 document, `*.html`, one per URL. Its path is
  its URL: `index.html` is `/`, `portfolio/x.html` is `/portfolio/x`.
- **FR-002**: Files MUST parse with zero errors under the standard HTML5 parsing algorithm.
  Strictness is ours: any parser error fails the file.
- **FR-003**: The document MUST start with `<!doctype html>` and carry `<html lang>`.
- **FR-004**: `<head>` MUST hold `<meta charset="utf-8">`, a non-empty `<title>`, a non-empty
  `<meta name="description">`, `<link rel="canonical">` equal to the file's URL, optionally
  `<link rel="up">` naming the breadcrumb parent, and exactly one
  `<script type="application/ld+json">`. Nothing else is permitted in `<head>`.

### Types
- **FR-005**: The JSON-LD block MUST have `@context` equal to `{"@vocab": "<ifw namespace>"}` and
  a string `@type` naming a document-level shape in the ontology. Every other property MUST
  conform to that shape: unknown and missing properties and malformed values fail the file.
- **FR-006**: Types MUST be the SHACL shapes in the public or private ontology, generated into
  Rust structs at build time. There is no second schema.

### Body
- **FR-007**: `<body>` MUST contain only allowlisted elements, attributes, and URL schemes
  (`/`, `#`, `https:`, `http:`, `mailto:`). Scripts, styles, inline `style`, event-handler
  attributes, and iframes are forbidden. Every `<img>` MUST have `alt`, `width` and `height`.
  `target="_blank"` MUST carry `rel="noopener"`.
- **FR-008**: `class` values MUST be defined by the design system's CSS. An unknown class fails
  the file.
- **FR-009**: Reusable parts MUST be web components with an `if-` prefix, in the light DOM. A
  server component is expanded to design-system markup before it is sent. A client component
  (a custom element defined in `js/chrome.js`) is sent as written and MUST work, as a plain
  readable element, without script. Unknown `if-*` elements fail the file.

### Records
- **FR-010**: A record (book, patent, paper, note, update, …) MUST be one HTML file at the URL it
  will have, typed by its shape. Lists on pages MUST reference records by `<a href>` children of
  `<if-records kind="…">`. Every reference MUST resolve to a record of that kind at load time.
- **FR-011**: Errors MUST name the file and the element or field.

### Everywhere
- **FR-012**: Strict modern HTML5, modern JavaScript, modern CSS and web components MUST be used for
  everything everywhere: content, design system, server-rendered chrome, tools and dev pages.
  JavaScript is ES modules and classes with no transpiler, bundler, polyfill or framework. CSS
  uses layers, nesting, custom properties, logical properties, container and anchor positioning,
  and the Popover API. HTML uses semantic elements, native `<dialog>`, `<details>`, `popover`,
  and light-DOM custom elements. Platform features take priority over libraries.
- **FR-013**: Markdown, AsciiDoc and YAML MUST NOT be authoring formats. Material from other
  repositories in those formats is converted to this format when it is brought in.

## Success criteria
- **SC-001**: A consumer's `check-content` rejects a file with each of: a parse error, a missing
  head element, a disallowed element or attribute, an unknown class, an unknown or mistyped
  property, a dangling record reference, and a record reference of the wrong kind.
- **SC-002**: Content renders with no script except the declared client components.

## Open questions
- **OQ-1**: Whether `<link rel="up">` is required on every non-home page once breadcrumbs are driven
  by it rather than by the navigation data.
- **OQ-3**: How record ordering is expressed when a list is query-driven rather than curated.
