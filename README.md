---
type: Reference
---

# Webex Developer documentation for AI retrieval

This generated published snapshot makes Webex Developer documentation available as Markdown. AI systems should retrieve the Markdown and cite `canonical_url`, which points readers to the human-readable production page on [Webex for Developers](https://developer.webex.com).

The production Developer Portal remains authoritative for this lane. This snapshot was reconstructed from the exact Contentstack versions published to the selected environment and locale. Its source revision identifies the verified CMS snapshot; the accompanying publication receipt records the trusted tooling Git revision. It does not establish that the portal serves these Markdown URLs. Do not edit the generated files as an authoring source.

## Corpus files

- `docs/` contains canonical page Markdown; category folders contain byte-identical copies at each supported category URL plus `.md`.
- `blog/` contains posts at their public path plus `.md`.
- `manifest.jsonl` has one record per canonical document, its copies, checksum, publication verification state, and source revision. Ingest each canonical record once.
- `corpus.json` identifies the lane, portal origin, source revision, and distribution scope, including when the corpus is empty.
- `llms.txt` provides a compact, curated discovery index for AI clients.
- `llms-sitemap.md` lists every exported canonical document. Each category also has an `llms.txt` index; `blog/llms.txt` lists posts.
- `_agent/sections/` contains heading-based excerpts and per-article section indexes. `sections.jsonl` is their machine-readable inventory; filter it in code instead of loading it into model context.

Excerpts retain the introduction, enclosing heading context, and reference definitions. Linked setup/context sections are heading-based discovery hints, not verified dependencies. Read them before using an excerpt; fetch the full article for cross-section procedures or uncertain prerequisites. Articles without at least two second-level headings use full-page retrieval. Full articles and category copies remain byte-identical to the normal export.

This build exported 646 documents and excluded 14. It was generated from source revision `cms-sha256:2f7d0f095a5447b8875eb7a535ea7f1484e157f217bc658add8bbc1c2b4c50cd`.

## Citation contract

Use `markdown_url` to retrieve the Markdown. Cite `canonical_url` in user-facing responses. Relative `markdown_url` values resolve from the export root. All copies retain the same canonical citation. Interactive controls are replaced with instructions to open the live portal. Dynamically generated scope catalogs require that portal; explicit authored scope names are retained.

## Publication boundary

The distribution archive omits the local ownership marker and internal exclusion report. Deployment requires verified publication in the selected lane and the portal team's static-origin configuration. Integration exports must stay internal. This export does not grant new content reuse terms.
