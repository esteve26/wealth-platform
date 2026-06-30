# DOCUMENTATION_CONVENTIONS

Document ID: PRJ-DOC-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Purpose

This document defines the conventions that govern all documentation within the Wealth Platform.

Its objective is to ensure that documentation remains:

* consistent;
* unambiguous;
* maintainable;
* AI-friendly;
* traceable;
* executable.

Every document in this repository must follow these conventions.

---

# 1. Documentation Principles

The documentation follows six principles:

1. Single Source of Truth
2. Explicit over Implicit
3. Architecture before Implementation
4. Business before Technology
5. AI Readability
6. Traceability

---

# 2. Single Source of Truth

Every concept must be defined exactly once.

Other documents may reference the definition but must not duplicate it.

Example:

| Concept              | Defining Document                |
| -------------------- | -------------------------------- |
| Workspace            | WEALTH_MODEL.md                  |
| Position             | WEALTH_MODEL.md                  |
| Aggregate Ownership  | AGGREGATE_CATALOG.md             |
| Financial Engine     | FINANCIAL_ENGINE_ARCHITECTURE.md |
| Persistence Strategy | ENTITY_MAPPING.md                |

---

# 3. Document Lifecycle

Every document has one lifecycle state.

Allowed states:

| Status     | Meaning                                                     |
| ---------- | ----------------------------------------------------------- |
| Draft      | Under active development                                    |
| Accepted   | Approved and considered stable                              |
| Deprecated | Retained for historical reasons but no longer authoritative |

Only Accepted documents may be used as implementation references.

---

# 4. Versioning

Version numbers follow semantic intent rather than software releases.

| Version | Meaning                                      |
| ------- | -------------------------------------------- |
| 0.x     | Working draft                                |
| 1.0     | First accepted version                       |
| 1.x     | Clarifications and non-breaking improvements |
| 2.0     | Significant architectural revision           |

Accepted documents should not receive structural changes without increasing the major version.

---

# 5. Document Header

Every document must begin with:

```text
Document ID:
Version:
Status:
Owner:

Depends On:
```

Optional fields may be added when necessary.

---

# 6. Naming Conventions

## Documents

Use:

```text
UPPER_SNAKE_CASE.md
```

Examples:

```text
APPLICATION_SERVICES.md
ENTITY_MAPPING.md
QUALITY_STRATEGY.md
```

---

## Directories

Use:

```text
lower-kebab-case
```

Examples:

```text
03-architecture
04-data
01-domain
```

---

## Document IDs

Each document belongs to one namespace.

Examples:

| Prefix | Area              |
| ------ | ----------------- |
| PRJ    | Project           |
| DOM    | Domain            |
| LOG    | Logical           |
| ARCH   | Architecture      |
| DATA   | Data              |
| API    | API               |
| SEC    | Security          |
| OPS    | Operations        |
| TEST   | Quality & Testing |

Examples:

```text
ARCH-001
DATA-003
API-002
```

Document IDs must remain stable once assigned.

---

# 7. Cross References

Documents should reference other documents by filename.

Example:

```text
See ENTITY_MAPPING.md
```

Avoid duplicating information already defined elsewhere.

---

# 8. Terminology

Terminology is defined by the Ubiquitous Language.

No synonyms may be introduced.

Examples:

Correct:

* Workspace
* Container
* Position
* Financial Plan

Incorrect:

* Project
* Account (unless referring to a Container type)
* Investment Position
* Plan

---

# 9. Diagrams

Diagrams should be simple, text-based and version-control friendly.

Preferred formats:

* ASCII diagrams
* Mermaid (when necessary)

Avoid binary diagram formats.

---

# 10. Technology Independence

Business, Domain and Data documentation must not depend on implementation technologies unless the document explicitly belongs to the implementation layer.

Technology choices belong in architecture and infrastructure documentation.

---

# 11. AI Readability Rules

Documentation must:

* avoid ambiguity;
* define ownership explicitly;
* define responsibilities explicitly;
* avoid hidden assumptions;
* use deterministic terminology.

AI coding agents should be able to implement features without inferring architectural decisions.

---

# 12. Traceability

Every implementation artifact must be traceable to a Functional Specification.

Every Functional Specification must be traceable to its implementation artifacts.

Traceability rules are defined in:

```text
IMPLEMENTATION_TRACEABILITY.md
```

---

# 13. Change Rules

Accepted documents may receive:

* typo corrections;
* clarification improvements;
* reference updates.

Architectural changes require a new version and explicit review.

---

# 14. Repository Quality Gate

Before a document is marked as Accepted, it must satisfy:

* consistent terminology;
* no duplicated definitions;
* explicit ownership;
* complete references;
* implementation readiness;
* AI readability.

---

# 15. Responsibilities

## Product Owner

Owns business intent.

## Architect

Owns architectural consistency.

## AI Coding Agent

Implements documentation without introducing undocumented functionality.

---

# 16. Acceptance Criteria

This document is complete when:

* documentation conventions are explicit;
* naming conventions are defined;
* lifecycle rules are defined;
* traceability rules are referenced;
* AI documentation rules are documented.

---

# 17. Change Log

| Version | Description                        |
| ------- | ---------------------------------- |
| 1.0     | Initial documentation conventions. |
