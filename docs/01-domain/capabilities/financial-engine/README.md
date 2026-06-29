# FINANCIAL_ENGINE

Document ID: CAP-FIN-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Depends On

* PROJECT_CONSTITUTION.md
* PRODUCT_PRINCIPLES.md
* UBIQUITOUS_LANGUAGE.md
* WEALTH_MODEL.md
* BUSINESS_CAPABILITIES.md

---

# 1. Purpose

The Financial Engine owns every Valuation produced by the platform.

Other capabilities consume Valuations but never create or modify them.

The Financial Engine is the deterministic calculation engine of the Wealth Platform.

It is the only capability responsible for producing financial calculations.

All monetary values, valuations, performance metrics and progress calculations originate from the Financial Engine.

No other capability may perform financial calculations.

---

# 2. Responsibilities

Responsible for:

* portfolio valuation;
* position valuation;
* holding aggregation;
* performance calculations;
* allocation calculations;
* currency conversion;
* historical valuation;
* financial plan progress calculation;
* portfolio analytics.

Not responsible for:

* importing data;
* managing assets;
* managing portfolios;
* financial planning decisions;
* AI explanations.

---

# 3. Business Concepts

## Valuation

The calculated monetary value of a Position, Holding, Portfolio or Financial Plan.

---

## Performance

Deterministic calculation of investment returns over time.

---

## Allocation

Distribution of wealth across Assets, Asset Classes, Providers, Containers or Portfolios.

---

## Financial Metrics

Calculated indicators such as:

* Total Wealth
* ROI
* CAGR
* Allocation
* Diversification
* Cash Exposure
* Risk Metrics

---

# 4. Business Rules

### BR-001

The Financial Engine is the single source of truth for every financial calculation.

### BR-002

Calculations must be deterministic.

### BR-003

Equal inputs always produce equal outputs.

### BR-004

Every new Transaction triggers an automatic recalculation.

### BR-005

Historical valuations may be stored according to Workspace configuration.

### BR-006

Calculation logic must remain independent from AI.

### BR-007

Every calculation must be reproducible.

---

# 5. Capability Interfaces

Consumes:

* Assets
* Positions
* Holdings
* Portfolios
* Financial Plans
* Transactions
* Exchange Rates

Produces:

* Valuations
* Performance
* Allocations
* Progress
* Financial Metrics

---

# 6. Dependencies

Consumes services from:

* Asset Management
* Transaction Management
* Portfolio Management
* Financial Planning
* Provider Integration

Provides services to:

* Dashboard
* Financial Intelligence
* AI Assistant
* Reporting

---

# 7. Security Considerations

* Calculation algorithms must be versioned.
* Every calculation must be auditable.
* Historical calculations must remain reproducible.

---

# 8. AI Considerations

AI may:

* explain calculations;
* summarize results;
* compare scenarios.

AI must never:

* modify calculations;
* replace deterministic algorithms;
* invent financial values.

---

# 9. Acceptance Criteria

* Financial responsibilities clearly defined.
* Single source of truth established.
* Interfaces documented.
* Dependencies documented.

---

# 10. Open Questions

None.

---

# 11. Change Log

| Version | Description           |
| ------- | --------------------- |
| 0.1     | Initial specification |
