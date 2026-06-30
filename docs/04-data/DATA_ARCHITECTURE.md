# DATA_ARCHITECTURE

Document ID: ARCH-DATA-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* APPLICATION_SERVICES.md
* FINANCIAL_ENGINE_ARCHITECTURE.md

---

# 1. Purpose

This document defines the data architecture of the Wealth Platform.

It specifies:

* what information is persisted;
* data ownership;
* persistence responsibilities;
* derived state strategy;
* read models;
* consistency rules;
* AI implementation constraints.

This document is technology-independent.

---

# 2. Architectural Decisions

## DA-001 — Aggregate Ownership

Every persisted business object belongs to exactly one Aggregate.

Only the owning Aggregate may modify its persisted state.

---

## DA-002 — Single Owner

Every persistent data object has exactly one owning module.

No data object may have multiple owners.

---

## DA-003 — Derived Financial State

Derived financial state is owned exclusively by the Financial Engine.

Derived state may be regenerated.

---

## DA-004 — Immutable History

Historical business facts are immutable.

Transactions are never modified after processing.

Corrections generate new business events.

---

## DA-005 — Read Models

Read models are projections.

They are optimized for querying.

They never own business state.

---

# 3. Data Categories

All persistent data belongs to one of four categories.

---

## Master Data

Stable reference information.

Examples:

* Asset
* Provider
* Organization
* Workspace
* Identity

Characteristics:

* low mutation rate;
* referenced by other objects;
* authoritative source.

---

## Transactional Data

Immutable business facts.

Examples:

* Transaction
* Audit Record
* Notification Delivery
* Synchronization Log

Characteristics:

* append-only;
* historical;
* never recalculated.

---

## Derived Data

Calculated financial state.

Examples:

* Position
* Holding
* Portfolio Metrics
* Financial Plan Progress
* Allocation Metrics
* Performance Metrics

Characteristics:

* deterministic;
* regenerable;
* owned by Financial Engine.

---

## Projection Data

Optimized read models.

Examples:

* Dashboard View
* Search View
* Portfolio Summary
* Home Dashboard
* Cached Widget Data

Characteristics:

* read-only;
* disposable;
* regenerable.

---

# 4. Persistence Matrix

| Data Object             | Category      | Owner            | Persisted | Regenerable |
| ----------------------- | ------------- | ---------------- | --------- | ----------- |
| Workspace               | Master        | Workspace        | Yes       | No          |
| Identity                | Master        | Identity         | Yes       | No          |
| Organization            | Master        | Organization     | Yes       | No          |
| Provider                | Master        | Provider         | Yes       | No          |
| Asset                   | Master        | Asset            | Yes       | No          |
| Container               | Master        | Provider         | Yes       | No          |
| Portfolio               | Master        | Portfolio        | Yes       | No          |
| Financial Plan          | Master        | Planning         | Yes       | No          |
| Transaction             | Transactional | Transaction      | Yes       | No          |
| Audit Record            | Transactional | Audit            | Yes       | No          |
| Position                | Derived       | Financial Engine | Yes       | Yes         |
| Holding                 | Derived       | Financial Engine | Yes       | Yes         |
| Portfolio Metrics       | Derived       | Financial Engine | Yes       | Yes         |
| Financial Plan Progress | Derived       | Financial Engine | Yes       | Yes         |
| Dashboard View          | Projection    | Dashboard        | Optional  | Yes         |
| Search Index            | Projection    | Infrastructure   | Optional  | Yes         |

---

# 5. Data Ownership Rules

Each data object has:

* exactly one owner;
* exactly one persistence responsibility;
* exactly one modification path.

Other modules may read data through approved interfaces.

Direct modification is forbidden.

---

# 6. Write Strategy

Business writes always follow:

```text
Command
    ↓
Application Service
    ↓
Aggregate
    ↓
Repository
    ↓
Database
```

No business state may bypass this flow.

---

# 7. Read Strategy

Reads follow:

```text
Query
    ↓
Query Handler
    ↓
Read Model
    ↓
DTO
```

Read models may combine data from multiple modules.

They never modify state.

---

# 8. Derived State Strategy

Derived data is persisted because:

* recalculation may be expensive;
* dashboards require fast responses;
* reporting requires stable snapshots;
* historical analysis requires reproducible values.

Derived state must always be reproducible.

---

# 9. Consistency Model

The platform follows:

* strong consistency inside one Aggregate;
* transactional consistency inside one Application Service;
* eventual consistency across modules where appropriate.

Derived financial state must always become internally consistent after pipeline execution.

---

# 10. Repository Rules

Repositories:

* persist aggregates;
* retrieve aggregates;
* never contain business rules;
* never calculate financial values;
* never orchestrate workflows.

Repositories belong to one module only.

---

# 11. Database Independence

Business architecture must not depend on database implementation.

Concepts such as:

* tables;
* indexes;
* schemas;
* SQL;

are implementation concerns documented separately.

---

# 12. Data Lifecycle

Master Data

```text
Create
↓
Update
↓
Archive
```

Transactional Data

```text
Append
↓
Never Modify
↓
Never Delete
```

Derived Data

```text
Calculate
↓
Persist
↓
Recalculate
```

Projection Data

```text
Generate
↓
Refresh
↓
Discard
↓
Regenerate
```

---

# 13. Financial Data Rules

The following objects are authoritative:

* Transaction
* Asset
* Exchange Rate
* Planning Assumption

The following objects are derived:

* Position
* Holding
* Portfolio Metrics
* Goal Progress
* Performance Metrics

Derived objects must never become the source of truth.

---

# 14. Versioning Strategy

Business objects evolve through versioned migrations.

Historical business meaning must never be lost.

Breaking schema changes require explicit migration plans.

---

# 15. Backup Strategy

The platform prioritizes backup of:

1. Master Data.
2. Transactional Data.

Derived and Projection Data may be regenerated if required.

---

# 16. AI Implementation Rules

AI coding agents must:

* identify the owner of every persistent object;
* never introduce duplicate ownership;
* classify every new object into one data category;
* never persist temporary calculations;
* use repositories only for aggregate persistence;
* keep read models independent from aggregates.

---

# 17. Implementation Contract

## Responsibilities

This document defines:

* persistence ownership;
* persistence categories;
* write strategy;
* read strategy;
* consistency model;
* lifecycle rules.

## Allowed Dependencies

Persistence depends on:

* aggregates;
* repositories;
* database abstraction.

## Forbidden Dependencies

Persistence must not:

* contain business rules;
* duplicate financial calculations;
* bypass aggregate ownership;
* expose infrastructure details to the domain.

---

# 18. Acceptance Criteria

This document is complete when:

* every persistent object has one owner;
* data categories are defined;
* write/read strategies are documented;
* consistency rules are explicit;
* AI implementation rules are complete.

---

# 19. Change Log

| Version | Description                           |
| ------- | ------------------------------------- |
| 0.1     | Initial data architecture definition. |
