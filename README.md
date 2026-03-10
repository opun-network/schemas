# OPuN Schema Specification

Public schema specification for **Beckn Protocol** network extensions used by **OPuN**. This repository defines domain-specific schemas, JSON-LD contexts, and example payloads for OPuN-compliant networks.

## Overview

These schemas extend [Beckn Protocol v2.0.0](https://github.com/beckn/protocol-specifications) with domain-specific attributes and message shapes for:

- **Learning** — Courses, enrollments, progress, and certificates (L&D / training)
- **Livelihood** — Job opportunities, applications, interviews, offers, and employment fulfillment

All extensions use **JSON-LD** with alignment to [schema.org](https://schema.org) and Beckn core context for semantic interoperability.

## Repository Structure

```
schemas/
├── README.md                 # This file
├── docs/                     # Documentation for reviewers and implementers
│   └── USER_STORIES_LIVELIHOOD.md  # User stories and payload mapping (livelihood)
├── learning/                 # Learning domain (courses, enrollments, certificates)
│   └── v1/
│       ├── schema-extension/ # context.jsonld, vocab.jsonld, attributes.yaml
│       └── examples/         # Example payloads per Beckn flow (search, select, init, …)
└── livelihood/               # Livelihood domain (jobs, applications, hiring)
    └── v1/
        ├── schema-extension/ # context.jsonld, vocab.jsonld, attributes.yaml
        └── examples/        # Example payloads per Beckn flow (discover, search, init, …)
```

## Domains


| Domain         | Path             | Description                                                                        |
| -------------- | ---------------- | ---------------------------------------------------------------------------------- |
| **Learning**   | `learning/v1/`   | Course catalog, enrollment lifecycle, progress tracking, and certificate issuance. |
| **Livelihood** | `livelihood/v1/` | Job discovery, applications, interviews, offers, and employment fulfillment.       |


Each domain version contains:

- **schema-extension/** — Authoritative schema definition:
  - `context.jsonld` — JSON-LD `@context` (IRIs, prefixes, property mappings)
  - `vocab.jsonld` — RDF vocabulary and type definitions
  - `attributes.yaml` — Domain-specific attributes and scopes (Item, Fulfillment, etc.)
- **examples/** — Sample request/response payloads for each Beckn 2.0 flow (e.g. search, on_search, init, on_init).

## Documentation

- **[User stories and payload mapping (Livelihood)](docs/USER_STORIES_LIVELIHOOD.md)** — User stories for job seeker and employer, flow-to-file mapping, and update variants. 

## Using the Schemas

1. **Context URLs**
  Use the published `context.jsonld` URL for each domain in your `@context` or `schema_context`, for example:
  - Learning: `https://schema.opun.network/learning/v1/` (or your published base)
  - Livelihood: `https://schema.opun.network/livelihood/v1/`
2. **Validation**
  Validate payloads against the domain’s `context.jsonld` and `attributes.yaml` (and any tooling you use for YAML/JSON schema).
3. **Examples**
  See the `examples/` directory under each domain for flow-by-flow request/response samples.

## Versioning

- **Domain versions** live under `{domain}/v1/`. Future backward-incompatible changes would be released as `v2/` under the same domain.
- Schema files within a version (e.g. `context.jsonld`, `attributes.yaml`) may be updated in a backward-compatible way within that version.

## Related Specifications

- [Beckn Protocol v2.0.0](https://github.com/beckn/protocol-specifications)
- [Schema.org](https://schema.org)
- [DeDi Protocol](https://dedi.global) (for decentralized identity where applicable)

## License

This specification is made available under the MIT License (or as specified in the repository).