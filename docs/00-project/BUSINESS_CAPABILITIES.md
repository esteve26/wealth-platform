# BUSINESS_CAPABILITIES

Document ID: DOM-CAP-001  
Version: 0.1  
Status: Accepted  
Owner: Product & Architecture

## Depends On

- PROJECT_CONSTITUTION.md
- PROJECT_PHILOSOPHY.md
- PRODUCT_PRINCIPLES.md
- PRODUCT_VISION.md
- UBIQUITOUS_LANGUAGE.md

## Required By

- DOMAIN_MODEL.md
- DOMAIN_ONTOLOGY.md
- BOUNDED_CONTEXTS.md
- ARCHITECTURE_OVERVIEW.md
- MODULE_DEFINITION.md

---

# 1. Purpose

This document defines the business capabilities of the Wealth Platform.

A business capability represents **what the platform must be able to do**, independently of how it is implemented.

Business capabilities are stable over time and constitute the foundation for the domain model, software architecture and product roadmap.

---

# 2. Capability Hierarchy

```text
Wealth Platform

├── Workspace Management
├── Identity & Access Management
├── Portfolio Management
├── Asset Management
├── Transaction Management
├── Provider Integration
├── Financial Intelligence
├── Goal & Strategy Management
├── Tax Management
├── Dashboard & Reporting
├── Artificial Intelligence
├── Organization Management
├── Platform Administration
└── Platform Configuration
```

---

# 3. Capability Catalogue

## 3.1 Workspace Management

### Purpose

Manage the business boundary where users, portfolios, providers and settings coexist.

### Responsibilities

- Create workspaces
- Configure workspace settings
- Multi-tenant isolation
- Workspace preferences
- Default currency
- Default language
- Default country

---

## 3.2 Identity & Access Management

### Purpose

Control authentication, authorization and permissions.

### Responsibilities

- Authentication
- MFA
- Roles
- Permissions
- Invitations
- User assignment
- Session management
- Audit of sensitive actions

---

## 3.3 Portfolio Management

### Purpose

Manage investment portfolios and their lifecycle.

### Responsibilities

- Create portfolios
- Archive portfolios
- Portfolio objectives
- Portfolio strategies
- Portfolio composition
- Portfolio performance
- Portfolio allocation
- Portfolio comparison
- Portfolio history

---

## 3.4 Asset Management

### Purpose

Manage every supported asset class.

### Responsibilities

- Asset catalogue
- Asset classification
- Holdings
- Positions
- Asset valuation
- Historical prices
- Asset metadata
- Multi-currency support

Supported asset classes include:

- Cash
- Stocks
- ETFs
- Bonds
- Crypto
- Precious Metals
- Commodities
- Real Estate
- Private Equity
- Crowdlending
- Art & Collectibles
- Other tangible assets

---

## 3.5 Transaction Management

### Purpose

Maintain the immutable financial history.

### Responsibilities

- Buy
- Sell
- Deposit
- Withdrawal
- Dividend
- Interest
- Fees
- Transfers
- Salary
- Manual transactions
- Imported transactions

---

## 3.6 Provider Integration

### Purpose

Synchronize external financial providers.

### Responsibilities

- Connector lifecycle
- API integrations
- PSD2 integrations
- CSV imports
- Wallet synchronization
- Incremental synchronization
- Synchronization monitoring
- Error recovery

---

## 3.7 Financial Intelligence

### Purpose

Transform financial data into actionable information.

### Responsibilities

- Wealth calculation
- Profit & loss
- Performance analysis
- Asset allocation
- Portfolio allocation
- Risk analysis
- Historical evolution
- Forecast support
- Recommendation generation
- Explainability

---

## 3.8 Goal & Strategy Management

### Purpose

Help users achieve financial objectives.

### Responsibilities

- Goal definition
- Strategy definition
- Progress tracking
- Goal monitoring
- Goal notifications

---

## 3.9 Tax Management

### Purpose

Estimate tax impact.

### Responsibilities

- Country tax profiles
- Capital gains estimation
- Tax reports
- Fiscal configuration

---

## 3.10 Dashboard & Reporting

### Purpose

Provide configurable business insights.

### Responsibilities

- Dashboards
- Widgets
- Saved layouts
- CSV exports
- Custom metrics
- Historical visualizations

---

## 3.11 Artificial Intelligence

### Purpose

Explain and assist, never replace deterministic calculations.

### Responsibilities

- Explain recommendations
- Explain charts
- Explain indicators
- Natural language queries
- Dashboard assistance
- Financial education

Out of scope:

- Autonomous investment decisions
- Unexplained buy/sell advice

---

## 3.12 Organization Management

### Purpose

Support professional wealth managers.

### Responsibilities

- Organizations
- Client management
- Advisor assignment
- Delegated access
- Client permissions

---

## 3.13 Platform Administration

### Purpose

Operate the platform securely.

### Responsibilities

- User administration
- Provider administration
- Monitoring
- Audit
- Feature flags
- Subscription plans

---

## 3.14 Platform Configuration

### Purpose

Configure platform-wide behavior.

### Responsibilities

- Languages
- Countries
- Supported currencies
- Asset categories
- Tax engines
- Notification preferences

---

# 4. Capability Prioritization

## MVP

Critical capabilities:

- Workspace Management
- Portfolio Management
- Asset Management
- Transaction Management
- Provider Integration
- Financial Intelligence

## Phase 2

- Goal & Strategy Management
- Dashboard & Reporting
- Organization Management

## Phase 3

- Tax Management
- Artificial Intelligence
- Advanced Administration

---

# 5. Architectural Principles

Each capability should:

- expose a clear business API;
- own its business rules;
- minimize coupling with other capabilities;
- evolve independently whenever possible.

---

# 6. Traceability

| Capability | Primary Domain Documents |
|------------|--------------------------|
| Workspace Management | DOMAIN_MODEL, PERMISSION_MODEL |
| Portfolio Management | DOMAIN_MODEL, BUSINESS_RULES |
| Asset Management | DOMAIN_MODEL, DATA_MODEL |
| Provider Integration | CONNECTOR_ARCHITECTURE |
| Financial Intelligence | FINANCIAL_ENGINE |
| AI | AI_ARCHITECTURE |
| Tax Management | TAX_ENGINE |

---

# 7. Change Log

| Version | Description |
|---------|-------------|
| 0.1 | Initial definition of business capabilities |
