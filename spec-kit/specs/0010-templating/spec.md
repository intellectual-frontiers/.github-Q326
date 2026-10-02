# Feature Specification: Templating and layouts

**Spec ID:** 0010-templating · **Constitution:** 1.2.1 · **Status:** In progress. The namespaces, registry, layouts, fragment responses and authored head elements (FR-001 to FR-011)
are implemented; the templating constructs (FR-013 to FR-017, except `app-records` and `app-units`) and
HTML layouts (FR-012) are specified and not yet built.
**Governs:** content documents (spec 0008) and the layouts that frame them, on every Intellectual
Frontiers web property.

**Input:** The HTML that authors write tells the server which layout to use and how to assemble
the page, in a small declarative vocabulary that is itself valid HTML5 and is checked against the
ontology. Built as Bare Metal Software: no scripting language, no expression engine, no
interpolation syntax.

## Namespaces

- **FR-001**: Server-side directives MUST use the `app-` prefix: elements `app-*` and attributes
  `data-app-*`. They are consumed during rendering and MUST NEVER reach a browser.
- **FR-002**: Client web components MUST use the `if-` prefix, are shipped to the browser, and are
  defined by the design system (spec 0007). They pass through rendering unchanged.
- **FR-003**: Prefixes MUST be hyphenated so every name is valid HTML5 syntax: custom-element names
  for elements, `data-*` for attributes. A colon-qualified name (`app:layout`) is not used.
- **FR-004**: Every `app-*`, `data-app-*` and `if-*` name MUST be declared in a registry. An
  unknown name fails the file, naming it.
- **FR-005**: One output filter MUST assert that no `app-` or `data-app-` markup remains in any
  response body. A leak is a server error in debug builds, and is stripped and logged in release
  builds.

## Layouts

- **FR-006**: `<body data-app-layout="<name>">` selects a layout. When the attribute is absent, NO
  layout is applied: the document is served as written, so any content can be served without our
  chrome. Layout names are `if:Layout` individuals in the ontology; an unknown name fails the file.
- **FR-007**: The layouts are `default` (header, breadcrumb band where a trail exists, page, footer)
  and `bare` (header, page, footer; no breadcrumb band and no section menu). Further layouts are
  added as ontology individuals. There is no layout named `none`; absence is the way to ask for none.
- **FR-008**: `data-app-chrome` on `<body>` MAY hold space-separated flags `no-breadcrumbs`,
  `no-header`, `no-footer`, refining the `default` layout. It requires `data-app-layout="default"`.
- **FR-009**: A document with no layout MUST be served as a complete HTML5 document made of the
  head elements and the `<body>` attributes it declares (minus `data-app-*`) and its body with server
  components expanded. Nothing is injected: no stylesheet, script, analytics, preload or metadata.
- **FR-010**: `data-app-as="fragment"` on `<body>`, or a request carrying a `Datastar-Request` or
  `HX-Request` header, selects a fragment response: the body's rendered content with no document
  and no chrome.
- **FR-011**: A document that uses a layout MUST have its authored `<meta>` and `<link>` elements
  emitted in the page head, except the charset, the description and the canonical link, which the
  layout derives. An authored `<meta>` replaces the layout's default of the same `name`, `property`
  or `http-equiv`. The layout MUST NOT emit a second copy of anything the author supplied.
- **FR-012**: A layout MAY be an HTML document in a mount using the standard `<slot name="…">`; a
  page element fills it with `slot="…"`. The server composes slots in the light DOM, with no shadow
  DOM. An unknown slot name, or a required slot left empty, fails the file.

## Templating

- **FR-013**: `<app-include src="…">` MUST replace itself with the children of the referenced
  document's `<body>`. `src` follows RFC 3986 relative-reference rules from the including document's
  VFS URI (spec 0009), and only exposed mounts may be read. Depth is limited to 8 and a cycle fails the file.
- **FR-014**: `<app-field name="…" [of="…"]>` MUST output one typed property of a record as
  escaped text. `of` is a record URL; it defaults to the current record. The property MUST exist
  in the record's shape.
- **FR-015**: `<app-each kind="…" [where="…"] [sort="…"] [limit="…"]>` with one `<template>` child
  MUST render the template once per matching record. Inside it, `app-field` refers to the current
  record. `kind` names a content shape. `where` is one or more conditions joined by ` and `, each
  `prop = 'v'`, `prop != 'v'` or `has prop`. `sort` is `prop` or `prop desc`; ties break by
  record URL. `limit` is a positive integer.
- **FR-016**: `data-app-if="<condition>"` on any element MUST keep the element only when the
  condition holds for the current record. Conditions use the grammar of FR-013.
- **FR-017**: `<app-records kind="…">` with `<a href>` children renders a curated list of records
  in the order written; each href MUST resolve to a record of that kind. `<app-units>` renders the
  business units from the ontology.
- **FR-018**: Templating MUST NOT provide scripting, arithmetic, user-defined functions or text
  interpolation. All output is escaped.
- **FR-019**: Every template reference (kind, property, type, slot, include, record) MUST be
  checked against the ontology shapes and the store when content loads. Errors name the file and
  the element.
- **FR-020**: Every construct MUST be valid HTML5 and every file MUST still satisfy spec 0008.

## Success criteria
- **SC-001**: A file with an unknown `app-*`, `data-app-*`, `if-*` or layout name is rejected.
- **SC-002**: No rendered page, fragment or proxied document contains `app-` or `data-app-` markup.
- **SC-003**: Each layout renders correctly at 375, 768, 1024 and 1440 px, and a document with no
  layout is served with none of our chrome, assets or scripts injected.
- **SC-004**: An include cycle, an include deeper than 8, a field naming a property the shape lacks,
  and a `where` or `sort` over a missing or mistyped property are each rejected at load.
- **SC-005**: A fragment response contains the body content and no `<html>`, `<head>` or chrome.

## Open questions
- **OQ-1**: Serving HTML that does not meet the strict content rules (foreign HTML from another
  mount) with no layout; it needs a separate, sanitizing path.
- **OQ-2**: Whether built-in layouts also exist as HTML documents in the design system, so other
  consumers can reuse them without Rust.
- **OQ-3**: Whether `where` needs `or` and grouping, or `and` is enough.
- **OQ-4**: Pagination for `app-each` when a `limit` is not wanted.
