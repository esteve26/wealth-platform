# PORTFOLIO_AGGREGATE

Document ID: AGG-PORTFOLIO-001
Version: 1.0
Status: Draft
Owner: Domain Architecture

## Depends On

* Portfolio Management Capability
* DOMAIN_MODEL.md
* ENTITY_MAPPING.md
* FUNCTIONAL_SPECIFICATION_GUIDE.md

---

# 1. Purpose

The Portfolio Aggregate represents an independent investment portfolio within a Workspace.

It is the authoritative owner of the Portfolio lifecycle and guarantees the consistency of all Portfolio business rules.

The Portfolio Aggregate does not manage transactions, positions or financial calculations.

---

# 2. Aggregate Root

Portfolio

The Portfolio Aggregate Root is responsible for enforcing all business invariants related to Portfolio management.

---

# 3. Identity

| Attribute    | Type                 | Notes                       |
| ------------ | -------------------- | --------------------------- |
| portfolio_id | Portfolio Identifier | System generated, immutable |

The Portfolio Identifier uniquely identifies a Portfolio across the platform.

---

# 4. Ownership

Every Portfolio belongs to exactly one Workspace.

| Attribute    | Type                 |
| ------------ | -------------------- |
| workspace_id | Workspace Identifier |

Ownership cannot be modified after creation.

---

# 5. Attributes

| Attribute     | Type             | Required | Mutable |
| ------------- | ---------------- | :------: | :-----: |
| name          | Portfolio Name   |    Yes   |   Yes   |
| description   | Description      |    No    |   Yes   |
| base_currency | Currency         |    Yes   |    No   |
| status        | Portfolio Status |    Yes   |   Yes   |
| created_at    | Timestamp        |    Yes   |    No   |
| updated_at    | Timestamp        |    Yes   |   Yes   |
| archived_at   | Timestamp        |    No    |   Yes   |

---

# 6. Value Objects

The Portfolio Aggregate is composed of the following Value Objects.

## Portfolio Name

Represents the business name of the Portfolio.

Rules:

* required;
* unique within a Workspace;
* cannot be empty.

---

## Description

Optional business description.

---

## Currency

Defines the Portfolio reporting currency.

Rules:

* mandatory;
* immutable after creation.

---

## Portfolio Status

Allowed values:

* Active
* Archived

---

# 7. Aggregate Invariants

The Portfolio Aggregate shall always satisfy the following invariants.

## INV-001

A Portfolio belongs to exactly one Workspace.

---

## INV-002

Portfolio names are unique within the owning Workspace.

---

## INV-003

A Portfolio always has a Base Currency.

---

## INV-004

A Portfolio always has a valid Status.

---

## INV-005

A newly created Portfolio contains:

* no Assets;
* no Transactions;
* no Positions.

---

## INV-006

The Aggregate Root is the only component allowed to modify Portfolio state.

---

# 8. Aggregate Behaviour

The Aggregate exposes the following business operations.

| Operation | Description                |
| --------- | -------------------------- |
| create()  | Creates a new Portfolio    |
| rename()  | Changes the Portfolio name |
| archive() | Archives the Portfolio     |

No additional business operations are currently defined.

---

# 9. Domain Events

The Aggregate may publish the following Domain Events.

| Event             | Description                    |
| ----------------- | ------------------------------ |
| PortfolioCreated  | Portfolio successfully created |
| PortfolioRenamed  | Portfolio name changed         |
| PortfolioArchived | Portfolio archived             |

Publication strategy is implementation-specific.

---

# 10. Out of Scope

The Portfolio Aggregate does not own:

* Transactions
* Positions
* Holdings
* Performance calculations
* Financial metrics
* Tax calculations

Those responsibilities belong to other Aggregates or Domain Services.

---

# 11. Related Functional Specifications

| Functional Specification         |
| -------------------------------- |
| FS-PORTFOLIO-001_CreatePortfolio |

---

# 12. Related Operation Contracts

| Operation Contract               |
| -------------------------------- |
| OP-PORTFOLIO-001_CreatePortfolio |

---

# 13. Traceability

| Artifact                 | Reference            |
| ------------------------ | -------------------- |
| Capability               | Portfolio Management |
| Aggregate Root           | Portfolio            |
| Functional Specification | FS-PORTFOLIO-001     |
| Operation Contract       | OP-PORTFOLIO-001     |

---

# 14. Change Log

| Version | Description                             |
| ------- | --------------------------------------- |
| 1.0     | Initial Portfolio Aggregate definition. |
