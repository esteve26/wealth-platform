# PORTFOLIO_MANAGEMENT

**Document ID:** CAP-PORT-001
**Version:** 1.0
**Status:** Accepted
**Owner:** Product & Architecture

---

# Purpose

Portfolio Management is responsible for organizing owned Positions into logical investment portfolios that execute one or more Financial Plans.

A Portfolio is an investment execution instrument.

It is **not**:

* a bank account;
* a broker account;
* a Provider;
* a Container;
* a planning entity.

Planning belongs exclusively to Financial Planning.

---

# Business Problem

Users typically own assets distributed across multiple Providers, accounts and asset classes.

Without logical portfolios it is difficult to:

* understand investment allocation;
* measure performance;
* compare investment strategies;
* execute different financial objectives;
* organize wealth independently from financial institutions.

Portfolio Management solves this problem by allowing Positions to be grouped according to investment intent rather than physical location.

---

# Business Value

Portfolio Management enables:

* provider-independent investment organization;
* diversified investment strategies;
* portfolio performance analysis;
* allocation analysis;
* investment execution for Financial Plans;
* rebalancing support.

---

# Scope

This capability is responsible for:

* Portfolio lifecycle;
* Portfolio composition;
* Position assignment;
* Allocation structure;
* Portfolio categorization;
* Portfolio metadata.

This capability is **not** responsible for:

* Goals;
* Strategies;
* Milestones;
* Progress calculation;
* Asset definitions;
* Transaction processing;
* Financial calculations.

---

# Responsibilities

Portfolio Management owns:

* Portfolio;
* Portfolio Composition;
* Position Assignment;
* Allocation Model.

Portfolio Management references:

* Positions;
* Holdings;
* Assets;
* Financial Plans.

Portfolio Management consumes:

* Financial Engine calculations.

Portfolio Management exposes:

* Portfolio composition;
* Allocation;
* Investment structure;
* Portfolio metadata.

---

# Core Concepts

## Portfolio

A logical grouping of Positions organized for investment execution.

A Portfolio exists independently of Providers and Containers.

---

## Portfolio Composition

Defines which Positions belong to a Portfolio.

Composition never changes ownership.

---

## Position Assignment

Associates Positions with Portfolios.

Assignment affects reporting and planning but never modifies the Position itself.

---

## Allocation

Represents the distribution of Portfolio value across:

* Asset Classes;
* Assets;
* Regions;
* Currencies;
* Sectors;
* Risk categories.

Allocation values are calculated by the Financial Engine.

---

## Rebalancing

Represents the desired change in Portfolio composition.

Execution of rebalancing is outside the responsibility of this capability.

---

# Ownership Model

Portfolio Management owns:

* Portfolio
* Portfolio Composition
* Position Assignment

Portfolio Management references:

* Position
* Holding
* Asset
* Financial Plan

Portfolio Management depends on:

* Financial Engine

Portfolio Management exposes context to:

* Dashboard
* AI Assistant
* Financial Planning

---

# Domain Principles

* Portfolio is an execution instrument.
* Portfolio never owns planning concepts.
* Portfolio groups Positions.
* Portfolio is Provider-independent.
* Portfolio is Container-independent.
* Portfolio does not calculate financial truth.
* Portfolio composition never modifies ownership.

---

# Lifecycle

```text
Draft

↓

Active

↓

Archived
```

Archived Portfolios preserve historical integrity.

---

# Business Rules

| ID     | Rule                                                                     |
| ------ | ------------------------------------------------------------------------ |
| BR-001 | Every Portfolio belongs to exactly one Workspace.                        |
| BR-002 | A Portfolio groups Positions.                                            |
| BR-003 | A Portfolio may support one or more Financial Plans.                     |
| BR-004 | Portfolio composition never modifies Positions.                          |
| BR-005 | Portfolio performance is calculated exclusively by the Financial Engine. |
| BR-006 | Deleting or archiving a Portfolio never deletes Positions.               |
| BR-007 | Portfolio allocation is always derived from Positions.                   |
| BR-008 | Portfolio is independent of Providers and Containers.                    |

---

# Actors

* Individual Investor
* Financial Advisor
* Wealth Manager
* Family Office
* Administrator

---

# Domain Events

* PortfolioCreated
* PortfolioUpdated
* PortfolioArchived
* PositionAssignedToPortfolio
* PositionRemovedFromPortfolio
* PortfolioLinkedToFinancialPlan
* PortfolioUnlinkedFromFinancialPlan
* PortfolioRebalanced

---

# Dependencies

| Capability             | Relationship       |
| ---------------------- | ------------------ |
| Financial Planning     | Planning context   |
| Transaction Management | Position changes   |
| Asset Management       | Asset reference    |
| Financial Engine       | Calculations       |
| Dashboard & Reporting  | Presentation       |
| AI Assistant           | Explanation        |
| Workspace Management   | Ownership boundary |

---

# Permissions

| Action                           | Investor | Advisor | Wealth Manager | Family Office | Administrator |
| -------------------------------- | -------- | ------- | -------------- | ------------- | ------------- |
| View Portfolio                   | ✓        | ✓       | ✓              | ✓             | ✓             |
| Create Portfolio                 | ✓        | ✓       | ✓              | ✓             | ✓             |
| Edit Portfolio                   | ✓        | ✓       | ✓              | ✓             | ✓             |
| Archive Portfolio                | ✓        | ✓       | ✓              | ✓             | ✓             |
| Assign Positions                 | ✓        | ✓       | ✓              | ✓             | ✓             |
| Link Portfolio to Financial Plan | ✓        | ✓       | ✓              | ✓             | ✓             |

Permission enforcement is defined by Identity & Access Management.

---

# AI Considerations

AI may:

* explain Portfolio composition;
* explain allocation;
* explain diversification;
* explain performance;
* suggest potential rebalancing opportunities.

AI must never:

* modify Portfolio composition;
* execute rebalancing;
* assign Positions automatically;
* alter deterministic financial calculations.

---

# Acceptance Criteria

The capability is considered complete when:

* Portfolio lifecycle is fully defined.
* Portfolio ownership is clearly separated from Financial Planning.
* Business rules are deterministic.
* Dependencies are explicit.
* AI limitations are documented.
* The capability is aligned with WEALTH_MODEL and FINANCIAL_PLANNING.

---

# Impact Analysis

This specification aligns Portfolio Management with the introduction of Financial Planning as the primary planning capability.

Planning concepts are removed from Portfolio Management.

Affected documents:

* WEALTH_MODEL
* BUSINESS_CAPABILITIES
* FINANCIAL_PLANNING
* UBIQUITOUS_LANGUAGE

---

# Future Evolution

Future versions may include:

* Portfolio templates;
* Target allocation models;
* Automatic rebalancing workflows;
* Scenario comparison;
* Multi-plan allocation support;
* Tax-aware portfolio optimization.

---

# Change Log

| Version | Description                                                                                                                                              |
| ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.0     | Refactored Portfolio Management to align with Financial Planning. Portfolio is now defined as an execution capability rather than a planning capability. |
