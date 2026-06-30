# ENTITY_MAPPING

Document ID: DATA-MAP-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Depends On

* DATA_ARCHITECTURE.md
* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* SOLUTION_STRUCTURE.md

---

# 1. Purpose

This document defines how Domain Aggregates are mapped to persistent entities.

Its purpose is to provide enough information for human developers or AI coding agents to generate persistence code, ORM mappings, repositories and migrations without making architectural assumptions.

This document does not define SQL tables directly.

---

# 2. Mapping Principles

## EM-001 — Aggregate First

Persistence is derived from Aggregates.

Database objects must never drive the domain model.

---

## EM-002 — One Aggregate Owner

Each persistent entity belongs to exactly one owning module.

Only the owning module may modify it.

---

## EM-003 — Explicit Persistence Strategy

Every mapped entity must declare its persistence strategy.

Allowed strategies:

* CRUD
* Append Only
* Snapshot
* Projection
* Immutable

---

## EM-004 — Entity-Specific Identifiers

Generic `id` identifiers are not allowed.

Primary identifiers must use the entity-specific name.

Examples:

* workspace_id
* transaction_id
* portfolio_id
* position_id
* asset_id

---

## EM-005 — Derived State Is Regenerable

Derived financial entities may be persisted but must remain reproducible from authoritative inputs.

---

# 3. Identifier Convention

Every persistent entity uses this identifier format:

```text
<entity>_id
```

Examples:

| Entity         | Identifier        |
| -------------- | ----------------- |
| Workspace      | workspace_id      |
| Identity       | identity_id       |
| Organization   | organization_id   |
| Provider       | provider_id       |
| Container      | container_id      |
| Asset          | asset_id          |
| Transaction    | transaction_id    |
| Position       | position_id       |
| Portfolio      | portfolio_id      |
| Financial Plan | financial_plan_id |

Foreign references use the same identifier name.

Example:

```text
portfolio.financial_plan_id
```

---

# 4. Persistence Strategy Definitions

## CRUD

Entity can be created, updated and archived through normal business operations.

Used for:

* Workspace
* Organization
* Provider
* Asset
* Portfolio
* Financial Plan

---

## Append Only

Entity represents immutable historical facts.

Records are added but never modified to change business meaning.

Used for:

* Transaction
* Audit Record

---

## Snapshot

Entity represents current derived state.

Snapshots may be replaced by deterministic recalculation.

Used for:

* Position
* Holding
* Portfolio Metrics
* Financial Plan Progress

---

## Projection

Entity is optimized for reading.

Projection data is disposable and regenerable.

Used for:

* Dashboard View
* Search View
* Reporting View

---

## Immutable

Entity must never be modified after creation.

Used for:

* Audit Record
* Compliance Event

---

# 5. Core Entity Mapping Catalog

| Aggregate      | Persistent Entity   | Owner Module    | Strategy    | Regenerable |
| -------------- | ------------------- | --------------- | ----------- | ----------- |
| Workspace      | WorkspaceEntity     | Workspace       | CRUD        | No          |
| Identity       | IdentityEntity      | Identity        | CRUD        | No          |
| Organization   | OrganizationEntity  | Organization    | CRUD        | No          |
| Provider       | ProviderEntity      | Provider        | CRUD        | No          |
| Container      | ContainerEntity     | Provider        | CRUD        | No          |
| Asset          | AssetEntity         | Asset           | CRUD        | No          |
| Transaction    | TransactionEntity   | Transaction     | Append Only | No          |
| Position       | PositionEntity      | FinancialEngine | Snapshot    | Yes         |
| Holding        | HoldingEntity       | FinancialEngine | Snapshot    | Yes         |
| Portfolio      | PortfolioEntity     | Portfolio       | CRUD        | No          |
| Financial Plan | FinancialPlanEntity | Planning        | CRUD        | No          |
| Document       | DocumentEntity      | Document        | CRUD        | No          |
| Tax Profile    | TaxProfileEntity    | Tax             | CRUD        | No          |
| Audit Record   | AuditRecordEntity   | Audit           | Immutable   | No          |
| Notification   | NotificationEntity  | Notification    | CRUD        | No          |

---

# 6. Aggregate Root Mapping

Every Aggregate has exactly one Aggregate Root.

The Aggregate Root is mapped to exactly one Root Entity.

The Root Entity is responsible for:

- aggregate persistence;
- optimistic concurrency;
- lifecycle management;
- aggregate consistency.

| Aggregate | Root Entity |
|-----------|-------------|
| Workspace | WorkspaceEntity |
| Identity | IdentityEntity |
| Organization | OrganizationEntity |
| Provider | ProviderEntity |
| Asset | AssetEntity |
| Transaction | TransactionEntity |
| Portfolio | PortfolioEntity |
| Financial Plan | FinancialPlanEntity |
| Position | PositionEntity |
| Holding | HoldingEntity |
| Document | DocumentEntity |
| Notification | NotificationEntity |
| Audit | AuditRecordEntity |
| Tax Profile | TaxProfileEntity |

---

# 7. Aggregate Composition

Aggregates may contain additional owned persistence entities.

These entities never exist independently.

Examples:

Portfolio Aggregate

- PortfolioEntity
- PortfolioPositionEntity
- PortfolioTargetAllocationEntity
- PortfolioStrategyEntity

Financial Plan Aggregate

- FinancialPlanEntity
- FinancialGoalEntity
- PlanningAssumptionEntity

Organization Aggregate

- OrganizationEntity
- OrganizationMemberEntity

Workspace Aggregate

- WorkspaceEntity
- WorkspaceMemberEntity

Provider Aggregate

- ProviderEntity
- ContainerEntity
- SynchronizationEntity

---

# 8. Owned Entity Rules

Owned Entities belong exclusively to their Aggregate Root.

They:

- have no independent lifecycle;
- cannot be loaded independently;
- cannot exist without their Aggregate Root;
- are persisted together with the Aggregate.

AI coding agents should map Owned Entities using the ORM owned entity capabilities whenever supported.

Examples:

PortfolioEntity

owns

- PortfolioSettings
- PortfolioPreferences
- PortfolioBenchmark

FinancialPlanEntity

owns

- PlanningAssumptions
- PlanningConfiguration

---

# 9. Financial Engine Entity Mapping

The Financial Engine owns all derived financial state.

Mapped entities:

| Entity                      | Strategy | Source of Truth                    |
| --------------------------- | -------- | ---------------------------------- |
| PositionEntity              | Snapshot | Transactions                       |
| HoldingEntity               | Snapshot | Positions                          |
| PortfolioMetricsEntity      | Snapshot | Positions + Portfolio              |
| FinancialPlanProgressEntity | Snapshot | Portfolio Metrics + Financial Plan |
| PerformanceMetricEntity     | Snapshot | Transactions + Valuations          |
| AllocationMetricEntity      | Snapshot | Positions + Holdings               |

Rules:

* These entities are never manually edited.
* These entities are recalculated by the Financial Engine.
* These entities may be deleted and rebuilt.
* These entities are not the source of financial truth.

---

# 10. Transaction Entity Mapping

## TransactionEntity

Owner:

* Transaction module

Strategy:

* Append Only

Identifier:

* transaction_id

Required references:

* workspace_id
* container_id
* asset_id, when applicable

Rules:

* Transactions are immutable after processing.
* Corrections require compensating transactions.
* Transaction history must remain reproducible.

---

# 11. Position Entity Mapping

## PositionEntity

Owner:

* FinancialEngine module

Strategy:

* Snapshot

Identifier:

* position_id

Required references:

* workspace_id
* container_id
* asset_id

Rules:

* Position is derived from Transactions.
* Position is persisted for performance.
* Position may be rebuilt from Transaction history.
* Users never modify Position directly.

---

# 12. Portfolio Entity Mapping

## PortfolioEntity

Owner:

* Portfolio module

Strategy:

* CRUD

Identifier:

* portfolio_id

Required references:

* workspace_id
* financial_plan_id

Rules:

* Portfolio owns structure and strategy.
* Portfolio does not own valuation.
* Portfolio does not own performance.
* Financial metrics belong to Financial Engine.

---

# 13. Financial Plan Entity Mapping

## FinancialPlanEntity

Owner:

* Planning module

Strategy:

* CRUD

Identifier:

* financial_plan_id

Required references:

* workspace_id

Rules:

* Only one Financial Plan may be active per Workspace.
* Financial Plan owns goals and assumptions.
* Progress calculations belong to Financial Engine.

---

# 14. Repository Mapping Rules

Each aggregate has one repository interface inside its owning module.

Example:

```text
Modules/Portfolio/Application/
    IPortfolioRepository.cs
```

Implementation lives in:

```text
Modules/Portfolio/Infrastructure/Repositories/
    PortfolioRepository.cs
```

Rules:

* repositories persist aggregates;
* repositories never contain business rules;
* repositories never calculate financial values;
* repositories never modify another module's entities.

---

# 15. ORM Mapping Rules

ORM mapping belongs to Infrastructure.

Example:

```text
Modules/Portfolio/Infrastructure/Persistence/
    PortfolioEntityConfiguration.cs
```

Rules:

* domain entities must not depend on ORM attributes;
* persistence configuration must not contain business rules;
* mapping must preserve aggregate boundaries;
* generated migrations must follow this mapping.

---

# 16. Cross-Module Reference Rules

Cross-module relationships are stored as identifiers, not object graphs.

Example:

```text
PortfolioEntity.financial_plan_id
```

Allowed:

* storing foreign identifiers;
* querying other modules through application interfaces;
* using read models for combined views.

Forbidden:

* loading another module's aggregate for mutation;
* cascading writes across module boundaries;
* exposing another module's internal persistence model.

---

# 17. AI Implementation Rules

AI coding agents must:

* generate one persistence mapping per persistent entity;
* use entity-specific identifiers;
* assign every entity to exactly one module;
* apply the documented persistence strategy;
* avoid generic `id` columns;
* generate repository interfaces and implementations;
* generate persistence tests;
* never infer ownership from table relationships.

---

# 18. Implementation Contract

## Responsibilities

This document defines:

* aggregate-to-entity mapping;
* persistence ownership;
* persistence strategy;
* identifier conventions;
* repository placement;
* ORM mapping placement.

## Required Output

For every mapped aggregate, implementation must generate:

* persistent entity;
* repository interface;
* repository implementation;
* ORM configuration;
* migration;
* persistence tests.

## Forbidden Output

AI agents must not generate:

* generic `id` columns;
* shared repositories for multiple modules;
* business rules inside persistence mappings;
* financial calculations inside repositories;
* cross-module write access.

---

# 19. Acceptance Criteria

This document is complete when:

* every core aggregate has a persistence mapping;
* every persistent entity has one owner;
* every persistent entity has a strategy;
* identifier conventions are explicit;
* AI implementation rules are actionable.

---

# 20. Change Log

| Version | Description                           |
| ------- | ------------------------------------- |
| 0.1     | Initial entity mapping specification. |
