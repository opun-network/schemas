# Learning Domain — Schema Extension (v1)

This directory contains the **Learning** domain schema extension for OPuN networks on Beckn Protocol v2.0. It defines the JSON-LD context, vocabulary, and domain-specific attributes for courses, enrollments, progress, and certificates.

## Files

| File             | Description |
|------------------|-------------|
| **context.jsonld** | JSON-LD `@context`: term definitions, prefixes (`opun`, `beckn`, `schema`), and property/type mappings for the learning domain. |
| **vocab.jsonld**   | RDF vocabulary: types and terms used in learning payloads. |
| **attributes.yaml** | Domain-specific attributes with types, scopes (Item, Fulfillment, etc.), and examples. |

## Domain Context

- **Base IRI:** `https://schema.opun.network/learning/v1/`
- **Domain in messages:** `opun:learning`

## Key Types and Entities

- **Course (Item)** — `LearningCourse`, `CourseCategory`, `CourseLevel`, `CourseType`, `CourseStatus`; attributes such as `courseCode`, `courseName`, `courseDescription`, `courseCategory`, `courseLevel`, `duration`, `schedule`, `feeAmount`, `prerequisites`, `learningObjectives`, `certificateTemplateId`, `accessibilityMetadata`.
- **Enrollment** — `LearningEnrollmentAttributes`: `enrollmentId`, `enrollmentStatus`, `enrollmentStage`, `formResponseId`, `prerequisiteVerification`, `enrollmentMetadata`.
- **Fulfillment / Progress** — `LearningFulfillmentAttributes`: `progressPercentage`, `completionDate`, `certificate` (e.g. `certificateId`, `certificateNumber`, `certificateType`, `certificateStatus`, `issueDate`).

## Attribute Scopes

Attributes are scoped for use in Beckn messages:

- **Item** — Course descriptor and catalog (e.g. `courseCode`, `courseName`, `courseLevel`, `feeAmount`).
- **Fulfillment** — Enrollment progress and certificate (e.g. `progressPercentage`, `certificate`, `completionDate`).
- **Price** — Fee-related (e.g. `feeAmount`, `currency`).

Use `attributes.yaml` for the full list and allowed values (enums).

## Usage

1. **In request/response payloads:** Include this extension’s context in `@context` or `schema_context`, e.g. the published URL for `context.jsonld`.
2. **Validation:** Validate payloads against the terms and structures defined in `context.jsonld` and `vocab.jsonld`, and attribute rules in `attributes.yaml`.

See the [examples/](../examples/README.md) directory for flow-wise sample payloads (search, select, init, confirm, status, update, cancel).
