# IMPLEMENTATION_TRACEABILITY

Document ID: PRJ-TRACE-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Purpose

This document defines the traceability model of the Wealth Platform.

Its purpose is to ensure that every business requirement can be traced to its corresponding implementation artifacts and that every implementation artifact can be traced back to a business requirement.

This document also defines the implementation workflow that AI coding agents must follow.

---

# 1. Traceability Philosophy

The platform follows four principles:

1. Every business requirement must have an implementation.
2. Every implementation must have a business justification.
3. Every implementation artifact must be traceable.
4. AI agents must never implement functionality without traceability.

---

# 2. Traceability Chain

Every feature follows the same lifecycle.

```text
Business Vision
        ↓
Functional Specification
        ↓
Acceptance Criteria
        ↓
Domain Aggregate
        ↓
Application Service
        ↓
Persistent Entity
        ↓
API Endpoint
        ↓
Frontend Screen
        ↓
Automated Tests
```

No step may be skipped.

---

# 3. Implementation Workflow

Every new feature must be implemented using the following order:

1. Functional Specification
2. Ubiquitous Language
3. Aggregate definition
4. Aggregate ownership validation
5. Application Service
6. Entity Mapping
7. Repository
8. API Endpoint
9. Frontend
10. Automated Tests
11. Documentation update

AI coding agents must follow this workflow.

---

# 4. Traceability Matrix

Each Functional Specification must be traceable to the following implementation artifacts.

| Artifact                        | Mandatory |
| ------------------------------- | --------- |
| Functional Specification        | Yes       |
| Aggregate                       | Yes       |
| Aggregate Owner                 | Yes       |
| Application Service             | Yes       |
| Repository                      | Yes       |
| Persistent Entity               | Yes       |
| API Endpoint                    | Yes       |
| Frontend Screen (if applicable) | Yes       |
| Unit Tests                      | Yes       |
| Integration Tests               | Yes       |
| UI Tests (if applicable)        | Yes       |
| Documentation Updates           | Yes       |

---

# 5. Completeness Rules

A Functional Specification is considered implemented only when every mandatory artifact exists.

Example:

```text
FS-PORTFOLIO-001

✓ Aggregate
✓ Application Service
✓ Repository
✓ Entity Mapping
✓ API Endpoint
✓ Unit Tests
✓ Integration Tests
✓ Documentation

Status

IMPLEMENTED
```

Example of an incomplete implementation:

```text
FS-PORTFOLIO-002

✓ Aggregate
✓ Application Service
✓ Repository
✗ API Endpoint
✓ Tests

Status

INCOMPLETE
```

---

# 6. Bidirectional Traceability

Traceability must work in both directions.

Business → Implementation

```text
Functional Specification
        ↓
Aggregate
        ↓
Service
        ↓
Entity
        ↓
Endpoint
```

Implementation → Business

```text
Endpoint
        ↓
Application Service
        ↓
Aggregate
        ↓
Functional Specification
```

Every implementation artifact must identify its originating Functional Specification.

---

# 7. AI Implementation Workflow

Before implementing a feature, an AI coding agent must identify:

* Functional Specification identifier;
* owning Aggregate;
* owning Application Service;
* persistent entity;
* repository;
* API endpoint;
* required tests.

Only after this analysis may implementation begin.

---

# 8. Required Deliverables

Every completed feature must include:

* backend implementation;
* persistence implementation;
* API implementation;
* automated tests;
* updated documentation.

Where applicable:

* frontend implementation;
* UI tests;
* reports;
* notifications.

---

# 9. Traceability Validation

A feature review must verify:

* every Functional Specification is implemented;
* no orphan Aggregates exist;
* no orphan API endpoints exist;
* no orphan database entities exist;
* no orphan frontend screens exist.

Orphan implementation artifacts are not permitted.

---

# 10. Reading Order for AI Coding Agents

AI coding agents should read documentation in the following order:

1. PROJECT_CONSTITUTION.md
2. IMPLEMENTATION_TRACEABILITY.md
3. Functional Specifications
4. Ubiquitous Language
5. DOMAIN_ARCHITECTURE.md
6. AGGREGATE_CATALOG.md
7. APPLICATION_SERVICES.md
8. DATA_ARCHITECTURE.md
9. ENTITY_MAPPING.md
10. API documentation
11. QUALITY_STRATEGY.md

This order minimizes implementation ambiguity.

---

# 11. Responsibilities

## Product Owner

Responsible for:

* Functional Specifications;
* Acceptance Criteria;
* business priorities.

---

## Architect

Responsible for:

* Domain Model;
* Application Architecture;
* Data Architecture;
* implementation consistency.

---

## AI Coding Agent

Responsible for:

* implementing approved requirements;
* preserving architecture;
* generating tests;
* updating documentation.

The AI coding agent must not introduce new business functionality that is not described in the documentation.

---

# 12. Forbidden Practices

The following are prohibited:

* implementing undocumented features;
* creating Aggregates without Functional Specifications;
* exposing APIs without Application Services;
* persisting entities without ownership;
* creating tests without business requirements;
* modifying business behavior without updating documentation.

---

# 13. Acceptance Criteria

This document is complete when:

* every implementation artifact is traceable;
* the implementation workflow is defined;
* completeness rules are explicit;
* AI implementation responsibilities are documented.

---

# 14. Change Log

| Version | Description                                     |
| ------- | ----------------------------------------------- |
| 0.1     | Initial implementation traceability definition. |
