# Feature Specification: Virtual file system (VFS)

**Spec ID:** 0009-vfs · **Constitution:** 1.2.1 · **Status:** Implemented in `www.intellectualfrontiers.com` (spec 003); open questions below remain
**Governs:** how every Intellectual Frontiers web property addresses, reads and serves content.

**Input:** Content comes from anywhere (a local directory, a git repository, later object storage)
and is addressed by one logical URI. Built as Bare Metal Software: our own small, tested
implementation, with OpenDAL studied for its design and not depended on.

## Addressing

- **FR-001**: A VFS URI MUST be a valid RFC 3986 URI of the form
  `vfs://<mount>/<path>[?rev=<rev>][#<fragment>]`: scheme `vfs`, the mount as the authority, a
  hierarchical path, `rev` as the only query parameter, and the fragment untouched.
- **FR-002**: A mount name MUST be lowercase `[a-z0-9-]`, 1 to 63 characters, and is
  case-normalized on input. The scheme is case-insensitive and normalized to `vfs`.
- **FR-003**: Paths MUST be normalized by RFC 3986 §5.2.4 dot-segment removal after decoding
  unreserved percent-escapes. A path that climbs above the mount root, or that contains an encoded
  `/`, `\` or NUL, MUST be rejected.
- **FR-004**: Relative references inside a VFS document MUST resolve by RFC 3986 §5. A reference
  that climbs above the mount root MUST be rejected, not clamped.
- **FR-005**: `?rev=` pins a revision (a git commit or an etag). A source that cannot honor a rev
  MUST refuse the request, never ignore it.

## Mounts

- **FR-006**: Each mount is a `if:ContentSource` individual in the ontology with a name, a source
  kind, a backing location that is itself a standard URI (`file:`, `https:`, `s3:`), an exposure
  (`none`, `assets`, `all`), and a rev policy. Public mounts live in the public ontology, private
  mounts in the private one. Credentials MUST NOT appear in the graph.
- **FR-007**: A deployment MAY override a mount's backing location with an environment variable
  `IF_MOUNT_<NAME>`.
- **FR-008**: Mounts MAY be layered: an overlay mount lists sources in precedence order, and the
  first source holding a path wins. A listing is the union with the same precedence.
- **FR-009**: Sources are read-only. Each declares its capabilities (list, rev, watch) and every
  source MUST pass the shared conformance tests.

## Serving

- **FR-010**: The server MUST proxy mounts at `/vfs/<mount>/<path>`, a direct mapping of the VFS
  URI. A mount's exposure decides what the proxy serves: `none` serves nothing and answers 404;
  `assets` serves non-HTML files; `all` also serves HTML.
- **FR-011**: Raw HTML source MUST NEVER be proxied. HTML under an `all` mount MUST pass the strict
  content parser and allowlist (spec 0008) and is served re-serialized from the sanitized tree.
- **FR-012**: The proxy MUST answer only an allowlist of content types, MUST set
  `X-Content-Type-Options: nosniff`, MUST send an `ETag` and honor `If-None-Match` with 304, and
  MUST mark pinned (`?rev=`) responses `immutable`.
- **FR-013**: Every `vfs://` URI in an outgoing `text/html`, `application/ld+json` or XML body, and
  in `Location` and `Link` headers, MUST be rewritten to `/vfs/<mount>/<path>[?query][#fragment]`
  by one central output filter, wherever it appears, including visible text and `srcset`. No
  `vfs:` URI reaches a browser.
- **FR-014**: A `vfs:` URI that cannot be parsed MUST fail the response in debug builds and be
  replaced and logged in release builds.
- **FR-015**: Content documents MAY use `vfs://` URIs in `href`, `src`, `srcset` and JSON-LD.
  At load time each MUST name an existing mount, an exposed path, and an existing file.

## Success criteria
- **SC-001**: The URI parser and resolver pass the RFC 3986 §5.4 normal examples.
- **SC-002**: Every rendered page contains no `vfs:` URI.
- **SC-003**: Path traversal attempts through the proxy, in any encoding, never read outside a mount.

## Open questions
- **OQ-1**: Byte-range requests for large assets.
- **OQ-2**: The git source (read a repository at a rev with the `git` CLI) and the snapshot refresh
  that uses it.
- **OQ-3**: Whether the `vfs` scheme is registered with IANA or stays private-use.
