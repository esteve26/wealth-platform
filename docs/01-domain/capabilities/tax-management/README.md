# TAX_MANAGEMENT

Document ID: CAP-TAX-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Depends On

* FINANCIAL_ENGINE
* TRANSACTION_MANAGEMENT
* PORTFOLIO_MANAGEMENT

---

# 1. Purpose

Tax Management supports tax-related calculations, reporting and planning.

It provides tax information while remaining independent from financial calculations performed by the Financial Engine.

Tax rules are country-specific and extensible.

---

# 2. Responsibilities

Responsible for:

* Responsible for deterministic tax calculations and tax reporting;
* realized gains;
* unrealized gains;
* tax lots;
* fiscal summaries;
* tax planning support.

Not responsible for:

* portfolio valuation;
* financial calculations;
* accounting.

---

# 3. Business Concepts

## Tax Profile

Configuration describing the applicable tax jurisdiction.

---

## Tax Lot

A taxable acquisition unit used to calculate gains and losses.

---

## Fiscal Event

A transaction producing tax consequences.

---

## Tax Report

Generated fiscal information.

---

# 4. Business Operations

* Calculate Tax Position
* Generate Tax Report
* Configure Tax Profile
* Recalculate Fiscal History

---

# 5. Business Rules

### BR-001

Tax calculations depend on the active Tax Profile.

### BR-002

Tax calculations are deterministic.

### BR-003

Fiscal history remains reproducible.

### BR-004

Tax rules may vary by jurisdiction.

### BR-005

Tax Management never modifies Transactions.

---

# 6. Capability Interfaces

Consumes:

* Transactions
* Portfolios
* Financial Engine

Produces:

* Tax Reports
* Tax Positions
* Fiscal Summaries

---

# 7. Dependencies

Consumes:

* Financial Engine
* Transaction Management
* Configuration

Provides:

* Dashboard
* Financial Intelligence
* AI Assistant

---

# 8. Security Considerations

* Fiscal information is confidential.
* Tax reports follow Workspace permissions.
* Generated reports are auditable.

---

# 9. AI Considerations

AI may:

* explain tax reports;
* explain fiscal concepts.

AI must never:

* calculate taxes;
* replace deterministic tax algorithms.

---

# 10. Acceptance Criteria

* Tax responsibilities documented.
* Tax concepts documented.
* Jurisdiction model defined.

---

# 11. Open Questions

Future versions will introduce a dedicated Tax Engine.

---

# 12. Change Log

| Version | Description           |
| ------- | --------------------- |
| 0.1     | Initial specification |
