# DOMAIN MODEL

Document ID: LOG-DM-000
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* UBIQUITOUS_LANGUAGE.md
* WEALTH_MODEL.md

---

# 1. Purpose

This directory contains the implementation-ready logical domain model of the Wealth Platform.

The purpose of these documents is to translate the conceptual business model into a precise and consistent domain model that can be implemented by software engineers or AI coding assistants without introducing additional architectural decisions.

Each document defines one business aggregate or one closely related group of business concepts.

---

# 2. Scope

The Domain Model defines:

* business entities;
* value objects;
* aggregate boundaries;
* ownership;
* relationships;
* business invariants;
* lifecycle;
* domain events;
* business operations.

The Domain Model does **not** define:

* persistence;
* database schemas;
* APIs;
* user interfaces;
* programming language implementation;
* infrastructure.

Those concerns are addressed in later project phases.

---

# 3. Structure

Each domain document follows the same structure.

## Purpose

Explains why the aggregate exists.

---

## Primary Business Entity

The central business concept of the aggregate.

This entity owns the aggregate lifecycle.

---

## Supporting Entities

Business entities that cannot exist independently of the primary entity.

---

## Value Objects

Immutable business concepts without identity.

Value Objects are compared by value rather than identity.

---

## Relationships

Business relationships with other aggregates.

Relationships describe collaboration, not ownership.

---

## Business Invariants

Rules that must always remain true.

An invariant may never be violated by any business operation.

---

## Lifecycle

Business states through which the aggregate evolves.

---

## Domain Events

Business facts that have already occurred.

Events describe completed business actions.

Events never represent commands or intentions.

---

## Business Operations

Operations allowed on the aggregate.

Operations describe business behaviour.

They do not prescribe technical implementation.

---

## Open Questions

Outstanding business decisions that affect the aggregate.

---

# 4. Domain Modeling Principles

## DM-001

Every aggregate has one clearly identified owner.

---

## DM-002

Every business concept has exactly one authoritative definition.

---

## DM-003

Ownership never crosses aggregate boundaries.

---

## DM-004

Aggregates collaborate through business concepts and domain events.

---

## DM-005

Business invariants always take precedence over implementation convenience.

---

## DM-006

Historical financial information is immutable.

---

## DM-007

Every aggregate belongs to exactly one Workspace.

---

## DM-008

Financial calculations are never performed inside business aggregates.

Aggregates delegate deterministic calculations to the Financial Engine.

---

# 5. Naming Conventions

The terminology defined in `UBIQUITOUS_LANGUAGE.md` is authoritative.

No alternative terminology may be introduced.

Entity names must be singular.

Examples:

* Position
* Portfolio
* Transaction
* Asset

Value Objects must also use singular names.

Examples:

* Money
* Percentage
* Allocation
* DateRange

Domain Events are named using the past tense.

Examples:

* TransactionRecorded
* PortfolioCreated
* GoalCompleted
* ProviderSynchronized

Business Operations use imperative verbs.

Examples:

* Create Portfolio
* Record Transaction
* Archive Document
* Synchronize Provider

---

# 6. Aggregate Collaboration Rules

Aggregates communicate only through:

* business references;
* published domain events;
* deterministic business services.

Aggregates never modify another aggregate's internal state directly.

---

# 7. Relationship with Capability Specifications

Capability Specifications define:

**What a business capability is responsible for.**

Domain Model documents define:

**How the business concepts inside that capability are structured.**

These documents complement each other.

Neither replaces the other.

---

# 8. Acceptance Criteria

The Domain Model is complete when:

* every business aggregate has been documented;
* ownership is unambiguous;
* invariants are explicit;
* business operations are defined;
* domain events are identified.

---

# 9. Domain Model Index

The following aggregates are expected:

* Workspace
* Organization
* Identity
* Provider
* Asset
* Transaction
* Position
* Financial Engine
* Portfolio
* Financial Plan
* Document
* Tax

Additional aggregates may be introduced if justified by business needs.

---

# 10. Change Log

| Version | Description                         |
| ------- | ----------------------------------- |
| 0.1     | Initial Domain Model specification. |
