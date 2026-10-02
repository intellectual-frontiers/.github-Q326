# Intellectual Frontiers ontology

> **Status: canonical and public.** The OWL knowledge graph for everything
> this repository (the Eidolon's public layer) says about Intellectual
> Frontiers. Seeded 2026-10-01 from the constitution, the six specs and the
> glossary; it names what they already say and adds no policy.

| File | Namespace | What it holds |
| --- | --- | --- |
| `if-core.ttl` | `https://www.intellectualfrontiers.com/ontology/core#` (`if:`) | The company, its five units (question, role, evidence, path, accent), decision options, evidence chain and taxonomy, registers, specs and glossary terms. |
| `if-web.ttl` | `https://www.intellectualfrontiers.com/ontology/web#` (`ifw:`) | Web content types. Each is an OWL class **and** a SHACL `NodeShape`; the site generates typed Rust from them. Imports core. |

## Who owns what

- **Public ontology and specs** live here and nowhere else.
- A **private** repository (today `www.intellectualfrontiers.com`) keeps its
  own `ontology/*.ttl` and `.specify/` specs, which `owl:imports` these IRIs
  and inherit this constitution. Private files may add; they must not
  redefine or remove anything declared here.

## Changing it

Same rule as the constitution: change it here, in a public commit, then
re-vendor downstream. A shape change is a content-contract change; the
consuming site's build will fail on content that no longer conforms, which is
the point.

## The SHACL subset the Rust generator reads

See the header of `if-web.ttl`. `sh:path`, `sh:datatype`, `sh:node`,
`sh:minCount`, `sh:maxCount`, `sh:in`, `sh:minLength`, `sh:order`, plus
`ifw:contentKind` to mark a document-level type.
