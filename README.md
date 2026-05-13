# Context-Ready Documentation — Demo

A prototype showing how a real Dynatrace documentation page can be restructured for AI consumption while remaining human-readable.

## What's here

- **[install-oneagent-linux.md](./install-oneagent-linux.md)** — A "context-ready" version of [Install OneAgent on Linux](https://docs.dynatrace.com/docs/ingest-from/dynatrace-oneagent/installation-and-operation/linux/installation/install-oneagent-on-linux), restructured with YAML frontmatter, typed chunks, and explicit relationships.

## What changed

The source page is well-crafted for human readers. This version preserves every fact and adds:

- **YAML frontmatter** — content type, audience, ownership, validation date, version range, and graph relationships made explicit.
- **Typed chunks** — each section carries a `chunk_type` (`permissions`, `resources`, `limitations`, `procedure`, `verification`, etc.) so retrieval can filter by intent.
- **Self-contained context** — every chunk restates its scope so it survives being retrieved out of order.
- **Typed edges** — hyperlinks become classified relationships: `permissions`, `related_concepts`, `runbook_uri`, `entity_refs`.

## A note on IDs

Concept, entity, and runbook IDs (`dt.concept.*`, `dt.entity.*`, `dt.runbook.*`) follow Dynatrace's naming convention but are illustrative. In production they would come from the canonical concept registry and Semantic Dictionary.

## The three principles

1. **Docs as data, not just prose.** Free text stays for humans; the envelope is for machines.
2. **Self-contained chunks beat better prompts.** Fix the substrate, not the LLM.
3. **Bind to the Semantic Dictionary.** Concept and entity references let an AI pivot from "what does this doc say" to "is this true in *your* environment right now."
