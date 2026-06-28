# PORTFOLIO_MANAGEMENT

Document ID: CAP-PORT-001  
Version: 0.1  
Status: Accepted  
Owner: Product & Architecture

## Depends On

- PROJECT_CONSTITUTION.md
- PRODUCT_PRINCIPLES.md
- PRODUCT_VISION.md
- UBIQUITOUS_LANGUAGE.md
- BUSINESS_CAPABILITIES.md
- WEALTH_MODEL.md

## Required By

- DOMAIN_MODEL.md
- DATA_MODEL.md
- FINANCIAL_ENGINE.md
- DASHBOARD_SYSTEM.md
- GOAL_STRATEGY_MANAGEMENT.md

---

# 1. Purpose

Portfolio Management is the business capability responsible for organizing wealth into meaningful investment structures.

A Portfolio is **not** a brokerage account, bank account or crypto exchange account.

A Portfolio is a logical business construct used to group Positions in order to pursue a financial objective.

---

# 2. Business Problem

Investors usually own assets distributed across multiple providers:

- banks
- brokers
- exchanges
- wallets
- real estate
- private investments

Traditional applications organise wealth by provider.

The Wealth Platform organises wealth by **investment purpose**.

This allows users to answer questions such as:

- How is my retirement strategy performing?
- Am I achieving my objectives?
- What is my current allocation?
- Am I taking more risk than expected?

---

# 3. Business Value

Portfolio Management provides:

- Strategic organisation of wealth.
- Separation between custody and investment strategy.
- Long-term performance measurement.
- Goal tracking.
- Asset allocation analysis.
- Risk monitoring.
- Decision support.

---

# 4. Scope

## Included

- Portfolio lifecycle.
- Portfolio composition.
- Position assignment.
- Objectives.
- Strategy.
- Performance.
- Historical evolution.
- Portfolio analytics.

## Excluded (Future Versions)

- Automatic rebalancing.
- Automated execution of trades.
- Robo-advisory.
- Tax optimisation.

---

# 5. Responsibilities

- Create portfolios.
- Update portfolios.
- Archive portfolios.
- Assign Positions.
- Remove Positions.
- Associate Goals.
- Associate Strategies.
- Calculate portfolio composition.
- Request financial calculations from the Financial Engine.
- Expose portfolio information to Dashboards and AI.

Portfolio Management does **not** calculate financial metrics directly.

---

# 6. Business Concepts

Primary concepts:

- Portfolio
- Position
- Holding
- Goal
- Strategy
- Workspace

Referenced concepts:

- Asset
- Transaction
- Provider
- Container

---

# 7. Domain Principles

## Portfolio is provider independent

A Portfolio never belongs to a broker.

It may contain Positions from multiple providers.

## Portfolio is objective driven

Every Portfolio exists to achieve one financial objective.

## Portfolio groups Positions

A Portfolio groups Positions.

It never owns Assets directly.

---

# 8. Lifecycle

```text
Draft
  ↓
Active
  ↓
Archived
```

Archived portfolios remain available for historical analysis.

Deletion is not supported.

---

# 9. Business Rules

- BR-001 — A Portfolio belongs to exactly one Workspace.
- BR-002 — A Portfolio may contain Positions from multiple Providers.
- BR-003 — A Portfolio may contain multiple Asset Classes.
- BR-004 — Archived Portfolios cannot receive new Positions.
- BR-005 — Historical performance must always remain available.
- BR-006 — Portfolios cannot be deleted.
- BR-007 — Every Portfolio should have one primary Goal.
- BR-008 — Portfolio valuation is calculated exclusively by the Financial Engine.

---

# 10. Actors

Primary:

- Individual Investor
- Wealth Manager
- Financial Advisor

Secondary:

- AI Assistant
- Platform Administrator

---

# 11. Main Use Cases

- Create Portfolio
- Configure Portfolio
- Assign Goal
- Define Strategy
- Add Positions
- Remove Positions
- View Performance
- Compare Portfolios
- Archive Portfolio
- View Historical Evolution

---

# 12. Domain Events

- PortfolioCreated
- PortfolioUpdated
- PortfolioArchived
- PositionAssigned
- PositionRemoved
- GoalAssigned
- StrategyAssigned

---

# 13. Dependencies

- Wealth Model
- Asset Management
- Transaction Management
- Financial Engine
- Goal & Strategy Management

---

# 14. Permissions

| Action | Owner | Advisor | Viewer |
|--------|:-----:|:-------:|:------:|
| View Portfolio | ✅ | ✅ | ✅ |
| Create Portfolio | ✅ | ✅* | ❌ |
| Update Portfolio | ✅ | ✅* | ❌ |
| Archive Portfolio | ✅ | ✅* | ❌ |
| Delete Portfolio | ❌ | ❌ | ❌ |

\* Subject to delegated permissions.

---

# 15. AI Considerations

AI may:

- Explain performance.
- Explain allocation.
- Explain diversification.
- Identify concentration risks.
- Answer portfolio questions.

AI must never:

- Modify a Portfolio.
- Execute transactions.
- Alter valuations.

---

# 16. Acceptance Criteria

- Portfolios can be created.
- Positions can be assigned.
- Historical information is preserved.
- Goals can be associated.
- Portfolio valuation is available.
- Multiple providers are supported.
- Multiple asset classes are supported.

---

# 17. Open Questions

| ID | Question |
|----|----------|
| OQ-001 | Can one Position belong to multiple Portfolios? |
| OQ-002 | Should Portfolio templates exist? |
| OQ-003 | Should archived Portfolios be restorable? |

---

# 18. Future Evolution

- Portfolio templates.
- Automatic rebalancing.
- Strategy simulation.
- Goal forecasting.
- Scenario analysis.
- Monte Carlo simulations.
- Tax-aware optimisation.

---

# 19. Change Log

| Version | Description |
|---------|-------------|
| 0.1 | Initial Portfolio Management capability specification |
