# MIGRATION_STRATEGY

Document ID: DATA-MIG-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Depends On

* DATA_ARCHITECTURE.md
* ENTITY_MAPPING.md
* SOLUTION_STRUCTURE.md
* QUALITY_STRATEGY.md

---

# 1. Purpose

This document defines how persistence models evolve over time in the Wealth Platform.

Its purpose is to ensure that schema changes, persistence changes and data transformations are safe, reviewable, testable and compatible with long-term product evolution.

Migrations are treated as part of the implementation contract, not as an incidental technical artifact.

---

# 2. Migration Principles

## MS-001 — Migration Follows Model Change

Every persistence model change that affects stored data must include a migration.

Code changes and persistence changes must remain synchronized.

---

## MS-002 — No Silent Data Loss

Migrations must never destroy business data silently.

Any destructive migration requires an explicit documented migration plan.

---

## MS-003 — Historical Meaning Is Preserved

Migrations must preserve the historical business meaning of existing records.

A migration may transform structure, but it must not rewrite the business truth.

---

## MS-004 — Migrations Are Reviewable

Every migration must be human-reviewable.

AI-generated migrations must be inspected before being accepted.

---

## MS-005 — Applied Migrations Are Immutable

Once a migration has been applied to any shared environment, it must not be edited.

Corrections require a new migration.

---

# 3. Migration Types

## Additive Migration

Adds new structures without changing existing data meaning.

Examples:

* adding a new persistent entity;
* adding a nullable property;
* adding a new projection;
* adding an index.

Preferred whenever possible.

---

## Transformational Migration

Changes the structure or meaning of persisted data while preserving business truth.

Examples:

* splitting one field into multiple fields;
* moving a property from one entity to another;
* normalizing an owned entity;
* introducing a new derived snapshot.

Requires explicit tests.

---

## Destructive Migration

Removes or overwrites persisted data.

Examples:

* dropping a persisted property;
* deleting historical records;
* changing identifiers;
* removing transaction history.

Forbidden unless explicitly approved and documented.

---

## Regeneration Migration

Rebuilds regenerable data from authoritative sources.

Examples:

* rebuilding Position snapshots;
* rebuilding Holdings;
* rebuilding Portfolio Metrics;
* rebuilding Dashboard projections.

Allowed only for data classified as regenerable in `DATA_ARCHITECTURE.md` or `ENTITY_MAPPING.md`.

---

# 4. Migration Safety Levels

| Safety Level | Description                                 | Approval                        |
| ------------ | ------------------------------------------- | ------------------------------- |
| Safe         | Additive and non-destructive                | Normal review                   |
| Controlled   | Transformational but reversible or testable | Architecture review             |
| Critical     | Destructive or business-sensitive           | Founder + Architecture approval |

---

# 5. Required Migration Metadata

Every migration must include:

* migration name;
* reason for change;
* affected modules;
* affected persistent entities;
* migration type;
* safety level;
* rollback strategy, where applicable;
* validation tests.

AI coding agents must generate this metadata alongside the migration.

---

# 6. Migration Naming Convention

Migration names must describe the business intent, not only the technical change.

Good examples:

```text
AddPortfolioTargetAllocation
IntroducePositionSnapshots
SplitTransactionSettlementDate
AddWorkspaceRetentionPolicy
```

Bad examples:

```text
UpdateDatabase
FixSchema
Migration1
Changes
```

---

# 7. Migration Generation Rules

Migrations must be generated only after:

1. The domain model change is defined.
2. The entity mapping is updated.
3. The persistence model is updated.
4. Tests are added or updated.

Migrations must not be generated from accidental code changes.

---

# 8. Migration Review Rules

Every migration review must verify:

* no unintended data loss;
* correct ownership module;
* correct affected entities;
* consistency with `ENTITY_MAPPING.md`;
* consistency with data categories;
* correctness of generated indexes and constraints;
* presence of validation tests.

---

# 9. Rollback Strategy

Rollback requirements depend on migration type.

## Additive Migration

Rollback is usually straightforward.

Example:

* remove added column;
* remove added table;
* remove added index.

---

## Transformational Migration

Rollback requires explicit reverse transformation or backup strategy.

---

## Destructive Migration

Rollback requires a documented recovery plan.

Destructive migrations must not rely on hope, manual reconstruction or incomplete backups.

---

# 10. Derived Data Regeneration

Derived financial state may be regenerated when:

* source Transactions remain intact;
* Assets remain intact;
* Exchange Rates remain intact;
* Financial Plans remain intact;
* required assumptions remain available.

Regeneration must be performed through the Financial Engine.

Direct database scripts must not recalculate financial state.

---

# 11. Projection Regeneration

Projection data may be deleted and rebuilt when:

* source data remains available;
* projection generation logic is deterministic;
* rebuild process is documented.

Projection regeneration must not affect business truth.

---

# 12. Identifier Migration Rules

Identifier migrations are considered critical.

Changing identifiers may affect:

* relationships;
* audit history;
* external references;
* documents;
* integrations.

Identifier migrations require explicit architecture approval.

Generic `id` columns are forbidden by `ENTITY_MAPPING.md`; migrations must preserve entity-specific identifiers.

---

# 13. Workspace Isolation During Migration

Migrations must preserve Workspace isolation.

Any migration affecting workspace-scoped data must ensure that:

* `workspace_id` remains present where required;
* data is not mixed across Workspaces;
* cross-workspace references are not introduced;
* tenant isolation is preserved.

---

# 14. AI Migration Rules

AI coding agents must:

* never generate destructive migrations without explicit instruction;
* never edit applied migrations;
* always generate migration tests;
* always explain why a migration is required;
* classify the migration type;
* classify the safety level;
* verify consistency with `ENTITY_MAPPING.md`;
* avoid physical database decisions not defined in architecture.

---

# 15. Migration Tests

Every migration must include tests appropriate to its type.

## Additive Migration Tests

Validate:

* schema creation;
* new fields can be persisted;
* existing data remains readable.

---

## Transformational Migration Tests

Validate:

* data transformation correctness;
* business meaning preservation;
* backward compatibility where required.

---

## Regeneration Migration Tests

Validate:

* derived data can be rebuilt;
* rebuilt values match deterministic expectations.

---

## Destructive Migration Tests

Validate:

* explicit approval exists;
* data loss is intentional;
* recovery strategy is documented.

---

# 16. Continuous Integration Requirements

CI must validate:

* migrations apply successfully;
* migrations do not break existing tests;
* persistence tests pass;
* integration tests pass;
* no migration introduces forbidden ownership violations;
* no migration introduces generic `id` identifiers.

---

# 17. Implementation Contract

## Responsibilities

This document defines:

* migration principles;
* migration types;
* migration safety levels;
* migration metadata;
* review rules;
* AI migration rules.

## Required Output

Every persistence-changing implementation must produce:

* updated entity mapping;
* migration;
* migration metadata;
* migration tests;
* updated documentation if ownership or persistence strategy changes.

## Forbidden Output

AI agents must not produce:

* silent destructive migrations;
* edited applied migrations;
* unreviewable migrations;
* migrations that bypass Aggregate ownership;
* migrations that recalculate financial state outside the Financial Engine.

---

# 18. Acceptance Criteria

This document is complete when:

* migration types are defined;
* safety rules are explicit;
* review requirements are documented;
* AI migration obligations are clear;
* destructive changes are controlled.

---

# 19. Change Log

| Version | Description                            |
| ------- | -------------------------------------- |
| 0.1     | Initial migration strategy definition. |
