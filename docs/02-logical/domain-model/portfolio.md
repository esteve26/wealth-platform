# PORTFOLIO

Document ID: LOG-DM-009
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* domain-model/README.md
* PORTFOLIO_MANAGEMENT Capability
* POSITION
* FINANCIAL_PLAN

---

# 1. Purpose

The Portfolio aggregate represents a logical grouping of Positions managed under a common investment strategy.

A Portfolio defines **how wealth is organized**, not **how wealth is calculated**.

Financial metrics, valuations and performance are produced by the Financial Engine and never owned by the Portfolio aggregate.

---

# 2. Aggregate Ownership

**Owning Capability:** Portfolio Management

The Portfolio aggregate owns the organizational structure of investments.

The Financial Engine owns every deterministic calculation associated with a Portfolio.

---

# 3. Primary Business Entity

## Portfolio

A Portfolio groups Positions according to a business objective or investment strategy.

Examples:

* Retirement Portfolio
* Long-Term Investments
* Dividend Portfolio
* Crypto Portfolio
* Real Estate Portfolio
* Liquidity Portfolio

A Portfolio exists independently of its current market value.

A Portfolio may temporarily contain no Positions.

---

# 4. Supporting Entities

## PortfolioPosition

Represents the assignment of a Position to a Portfolio.

Responsibilities:

* Position reference
* Allocation status
* Inclusion date

---

## PortfolioStrategy

Represents the intended investment strategy.

Examples:

* Growth
* Income
* Balanced
* Capital Preservation
* Passive Indexing
* High Risk

The strategy is descriptive.

It never performs calculations.

---

## TargetAllocation

Represents the desired allocation defined by the user.

Examples:

* 60% Equities
* 30% Bonds
* 10% Cash

Target allocations are planning objectives.

They are not calculated values.

---

# 5. Value Objects

## PortfolioId

Globally unique identifier.

---

## PortfolioName

Business name.

---

## PortfolioStatus

Possible values:

* Draft
* Active
* Archived

---

## InvestmentObjective

High-level business objective.

Examples:

* Wealth Growth
* Retirement
* Capital Preservation
* Income Generation

---

# 6. Relationships

Portfolio belongs to:

* Workspace
* Financial Plan

Portfolio references:

* Positions

Portfolio receives:

* Performance metrics from Financial Engine

Portfolio never owns:

* Positions
* Transactions
* Holdings
* Financial calculations

---

# 7. Business Invariants

## POI-001

Every Portfolio belongs to exactly one Workspace.

---

## POI-002

Every Portfolio belongs to exactly one Financial Plan.

---

## POI-003

A Position may belong to only one active Portfolio.

---

## POI-004

Portfolio structure is independent from Portfolio valuation.

---

## POI-005

Financial calculations never occur inside the Portfolio aggregate.

---

## POI-006

Target allocations are business intentions.

Actual allocations are calculated by the Financial Engine.

---

# 8. Lifecycle

```text
Draft
   │
   ▼
Active
   │
   ├──────────────┐
   ▼              │
Archived          │
```

Rules:

* Archived Portfolios are read-only.
* Historical allocations remain available.
* Archived Portfolios preserve investment history.

---

# 9. Domain Events

Published:

* PortfolioCreated
* PortfolioActivated
* PortfolioArchived
* PositionAssignedToPortfolio
* PositionRemovedFromPortfolio
* PortfolioStrategyChanged
* TargetAllocationChanged

Consumed:

* PositionRecalculated
* FinancialPlanCreated

---

# 10. Business Operations

Lifecycle

* Create Portfolio
* Activate Portfolio
* Archive Portfolio

Composition

* Assign Position
* Remove Position

Planning

* Change Strategy
* Update Target Allocation

---

# 11. Ownership Rules

Portfolio owns:

* Portfolio identity
* Portfolio lifecycle
* Position assignments
* Investment strategy
* Target allocation

Portfolio never owns:

* Position state
* Financial performance
* Market value
* Holdings
* Transactions

---

# 12. Implementation Constraints

Portfolio is a business aggregate.

It represents organizational intent rather than financial state.

All deterministic portfolio calculations are delegated to the Financial Engine.

Portfolio performance must always be reproducible from Position snapshots.

---

# 13. Acceptance Criteria

The Portfolio aggregate is complete when:

* organizational responsibilities are explicit;
* Position ownership remains external;
* strategy and target allocation are defined;
* financial calculations are excluded;
* relationships with Financial Plan are documented.

---

# 14. Open Questions

Future versions may support nested Portfolios.

This feature is intentionally outside the scope of version 1.

---

# 15. Change Log

| Version | Description                             |
| ------- | --------------------------------------- |
| 0.1     | Initial Portfolio aggregate definition. |
