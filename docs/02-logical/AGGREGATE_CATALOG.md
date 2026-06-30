# AGGREGATE CATALOG

Document ID: LOG-AGG-001
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* domain-model/README.md
* All Capability Specifications

---

# 1. Purpose

The Aggregate Catalog defines the complete set of business aggregates that compose the Wealth Platform domain.

Its purpose is to establish clear ownership boundaries before documenting each aggregate in detail.

This document is the entry point to the logical domain model.

---

# 2. Aggregate Definition

An Aggregate is a consistency boundary that groups one Primary Business Entity together with its supporting entities and value objects.

Each Aggregate:

* owns its business invariants;
* controls its internal consistency;
* exposes business operations;
* publishes domain events;
* collaborates with other aggregates through references and events.

---

# 3. Aggregate Catalog

| Aggregate      | Owner Capability        | Primary Business Entity |
| -------------- | ----------------------- | ----------------------- |
| Workspace      | Workspace Management    | Workspace               |
| Organization   | Organization Management | Organization            |
| Identity       | Identity & Access       | Identity                |
| Provider       | Provider Integration    | Provider                |
| Container      | Provider Integration    | Container               |
| Asset          | Asset Management        | Asset                   |
| Transaction    | Transaction Management  | Transaction             |
| Position       | Transaction Management  | Position                |
| Portfolio      | Portfolio Management    | Portfolio               |
| Financial Plan | Financial Planning      | Financial Plan          |
| Document       | Document Management     | Document                |
| Tax            | Tax Management          | Tax Profile             |

---

# 4. Aggregate Dependencies

The logical dependency graph is:

```text
Workspace
    │
    ├────────────┐
    ▼            ▼
Identity   Organization
    │            │
    └──────┬─────┘
           ▼
        Provider
           │
           ▼
       Container
           │
           ▼
         Asset
           │
           ▼
     Transaction
           │
           ▼
       Position
           │
           ▼
       Portfolio
           │
           ▼
    Financial Plan
```

Dependencies indicate business collaboration.

They do not imply ownership.

---

# 5. Ownership Rules

Every aggregate owns exactly one Primary Business Entity.

Business concepts never have multiple owners.

Ownership responsibilities are defined by the owning capability and refined in the corresponding domain model document.

---

# 6. Aggregate Communication

Aggregates communicate through:

* references to other aggregates;
* published domain events;
* deterministic domain services.

Aggregates never modify another aggregate directly.

---

# 7. Aggregate Evolution

Each aggregate may evolve independently provided that:

* published business contracts remain compatible;
* business invariants remain valid;
* ownership boundaries are preserved.

---

# 8. Relationship with the Domain Model

Each aggregate listed in this catalog has a dedicated document in the `domain-model` directory.

Those documents define:

* structure;
* invariants;
* lifecycle;
* business operations;
* domain events.

This catalog intentionally avoids implementation details.

---

# 9. Acceptance Criteria

The Aggregate Catalog is complete when:

* every aggregate is identified;
* ownership is explicit;
* dependency direction is clear;
* every aggregate has a corresponding domain model document.

---

# 10. Change Log

| Version | Description                |
| ------- | -------------------------- |
| 0.1     | Initial aggregate catalog. |
