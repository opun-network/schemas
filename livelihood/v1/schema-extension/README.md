# Livelihood Domain — Schema Extension (v1)

This directory contains the **Livelihood** domain schema extension for OPuN networks on Beckn Protocol v2.0. It defines the JSON-LD context, vocabulary, and domain-specific attributes for job opportunities, applications, interviews, offers, and employment fulfillment.

## Overview

The Livelihood schema extension enables:

- **Job discovery and catalog** — Search, filtering, and catalog publication of job opportunities
- **Application lifecycle** — Application forms, submission, status tracking, document management
- **Interview and assessment** — Interview scheduling, stages, types, and modes
- **Employment services** — Job offers, candidate profiles, and fulfillment tracking
- **Candidate experience** — Profile management, application tracking, and accessibility metadata

## Files in This Directory

| File             | Description |
|------------------|-------------|
| **context.jsonld** | JSON-LD `@context`: term definitions, prefixes (`opun`, `beckn`, `schema`), and property/type mappings for the livelihood domain. |
| **vocab.jsonld**   | RDF vocabulary: types and terms used in livelihood payloads. |
| **attributes.yaml** | Domain-specific attributes with types, scopes (Item, Fulfillment, etc.), and examples. |

## Directory Structure (this repo)

Within the schemas repository, the livelihood domain is laid out as:

```
livelihood/v1/
├── schema-extension/     # This directory
│   ├── README.md
│   ├── context.jsonld
│   ├── vocab.jsonld
│   └── attributes.yaml
└── examples/
    ├── cancel/
    ├── confirm/
    ├── discover/
    ├── init/
    ├── select/
    ├── status/
    ├── support/
    └── update/
```

## Domain: Livelihood

The Livelihood domain provides schemas for job opportunities, employment services, and related workflows.

### Key Entities

- **JobOpportunityAttributes**: Comprehensive job posting details including salary, skills, benefits, and application requirements
- **ApplicationFormAttributes**: Structured application forms with required fields and submission URLs
- **InterviewProcessAttributes**: Interview scheduling and process management including stages, types, and modes
- **ApplicationStatusAttributes**: Complete application tracking with status codes from submission to joining
- **CandidateProfileAttributes**: Job seeker profiles with resume, portfolio, experience, and preferences
- **LivelihoodJobOfferAttributes**: Detailed job offers with salary breakdowns, benefits, and employment terms
- **LivelihoodApplicationAttributes**: Application management with forms, documents, and submission tracking
- **LivelihoodFulfillmentAttributes**: End-to-end fulfillment tracking including verification, interviews, and status updates

### Core Flows

1. **Discovery**: Search and browse job opportunities using Beckn v2.0.0 discovery APIs with catalog publication
2. **Selection**: Select specific job opportunities and view detailed requirements
3. **Initialization**: Initialize the application process with candidate information
4. **Confirmation**: Confirm job applications and process submissions
5. **Status Tracking**: Monitor application status, interview schedules, and progress updates
6. **Updates**: Handle job offer responses, confirmation updates, and status changes
7. **Support**: Access customer support and assistance throughout the process
8. **Cancellation**: Cancel applications or withdraw from processes when needed

## Domain Context

- **Base IRI:** `https://schema.opun.network/livelihood/v1/`
- **Domain in messages:** `opun:livelihood`

## Usage

1. **In request/response payloads:** Include this extension’s context in `@context` or `schema_context` (e.g. the published URL for `context.jsonld`).
2. **Validation:** Validate payloads against the terms in `context.jsonld` and `vocab.jsonld`, and attribute rules in `attributes.yaml`.

See the [examples/](../examples/README.md) directory for flow-wise sample payloads (discover, search, select, init, confirm, status, update, support, cancel).

## Related Specifications

- [Beckn Protocol v2.0.0](https://github.com/beckn/protocol-specifications)
- [DeDi Protocol](https://dedi.global)
- [Schema.org](https://schema.org)
