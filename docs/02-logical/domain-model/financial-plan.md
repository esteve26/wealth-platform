# FINANCIAL_PLAN

Document ID: LOG-DM-010
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* domain-model/README.md
* FINANCIAL_PLANNING Capability
* PORTFOLIO

---

# 1. Purpose

The Financial Plan aggregate represents the long-term financial strategy of a Workspace.

It defines **why** wealth is managed, while Portfolios define **how** investments are organized.

A Financial Plan contains business objectives, planning assumptions and one or more Portfolios aligned to those objectives.

The Financial Plan never performs financial calculations.

---

# 2. Aggregate Ownership

**Owning Capability:** Financial Planning

The Financial Plan aggregate owns financial objectives, planning assumptions and strategic decisions.

Financial projections and scenario calculations are produced by the Financial Engine.

---

# 3. Primary Business Entity

## Financial Plan

A Financial Plan represents the strategic financial roadmap of a Workspace.

Examples:

* Personal Wealth Plan
* Retirement Plan
* Family Wealth Plan
* Corporate Treasury Plan

Each Workspace may maintain multiple Financial Plans over time, but only one Financial Plan may be Active at any given time.

---

# 4. Supporting Entities

## Financial Goal

Represents a measurable business objective.

Examples:

* Retirement
* University Education
* House Purchase
* Emergency Fund
* Financial Independence

Responsibilities:

* target amount;
* target date;
* priority;
* completion criteria.

---

## Planning Assumption

Represents assumptions used during planning.

Examples:

* Inflation
* Expected Return
* Savings Rate
* Retirement Age

These assumptions guide planning but never perform calculations.

---

## PortfolioAssignment

Represents the assignment of a Portfolio to a Financial Plan.

Responsibilities:

* Portfolio reference;
* assignment date;
* strategic role.

---

# 5. Value Objects

## FinancialPlanId

Globally unique identifier.

---

## FinancialPlanName

Business name.

---

## FinancialPlanStatus

Possible values:

* Draft
* Active
* Archived

---

## PlanningHorizon

Represents the planning period.

Examples:

* 10 Years
* 20 Years
* Lifetime

---

# 6. Relationships

Financial Plan belongs to:

* Workspace

Financial Plan references:

* Portfolios

Financial Plan contains:

* Financial Goals
* Planning Assumptions

Financial Plan receives:

* Progress metrics from Financial Engine

Financial Plan never owns:

* Portfolio calculations
* Position calculations
* Transaction history

---

# 7. Business Invariants

## FPI-001

Every Financial Plan belongs to exactly one Workspace.

---

## FPI-002

Only one Financial Plan may be Active per Workspace.

---

## FPI-003

Every Portfolio belongs to exactly one Financial Plan.

---

## FPI-004

Financial Goals belong to exactly one Financial Plan.

---

## FPI-005

Planning assumptions are business inputs.

Calculated projections belong to the Financial Engine.

---

## FPI-006

The Financial Plan never performs deterministic calculations.

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

* Archived Financial Plans become read-only.
* Historical Financial Plans remain available.
* Activating a new Financial Plan archives the previously active one.

---

# 9. Domain Events

Published:

* FinancialPlanCreated
* FinancialPlanActivated
* FinancialPlanArchived
* FinancialGoalCreated
* FinancialGoalUpdated
* FinancialGoalCompleted
* PlanningAssumptionChanged
* PortfolioAssignedToFinancialPlan

Consumed:

* PortfolioCreated
* PositionRecalculated

---

# 10. Business Operations

Lifecycle

* Create Financial Plan
* Activate Financial Plan
* Archive Financial Plan

Planning

* Create Financial Goal
* Update Financial Goal
* Complete Financial Goal
* Update Planning Assumptions

Portfolio Management

* Assign Portfolio
* Remove Portfolio

---

# 11. Ownership Rules

Financial Plan owns:

* Financial Plan lifecycle
* Financial Goals
* Planning Assumptions
* Portfolio assignments

Financial Plan never owns:

* Portfolios
* Positions
* Holdings
* Transactions
* Financial calculations

---

# 12. Implementation Constraints

The Financial Plan aggregate defines strategic intent.

Financial simulations, forecasts and progress calculations are delegated to the Financial Engine.

Business planning remains separated from deterministic financial computation.

---

# 13. Acceptance Criteria

The Financial Plan aggregate is complete when:

* strategic responsibilities are explicit;
* Financial Goals are defined;
* Portfolio relationships are documented;
* calculation responsibilities remain delegated;
* business invariants are explicit.

---

# 14. Open Questions

Future versions may support multiple active planning scenarios for comparative analysis.

This capability is intentionally outside the scope of version 1.

---

# 15. Change Log

| Version | Description                                  |
| ------- | -------------------------------------------- |
| 0.1     | Initial Financial Plan aggregate definition. |
