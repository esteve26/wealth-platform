# UBIQUITOUS_LANGUAGE

Document ID: DOM-UL-001
Version: 0.1
Status: Accepted
Owner: Product & Architecture

## Depends On

- PROJECT_CONSTITUTION.md
- PROJECT_PHILOSOPHY.md
- PRODUCT_PRINCIPLES.md
- PRODUCT_VISION.md

---

# Purpose

This document defines the official business vocabulary of the Wealth Platform.

Every document, diagram, database model, API, source code and AI prompt must use these definitions consistently.

If two terms could describe the same concept, this document is the authoritative source.

---

# Naming Rules

- One concept → One term.
- Avoid synonyms.
- Business terminology has priority over technical terminology.
- All official terms are written in English.
- UI translations may vary by language, but the domain term never changes.

---

# Core Concepts

| Term | Definition |
|------|------------|
| Workspace | Top-level business boundary that contains portfolios, users, providers, goals and settings. A workspace belongs to an individual or an organization. |
| User | A person authenticated in the platform. |
| Organization | A legal entity that manages one or more workspaces or client workspaces. |
| Portfolio | A logical collection of holdings created to achieve a financial objective. A holding may belong to multiple portfolios. |
| Holding | The quantity of an asset owned within a specific container or provider. |
| Asset | Any financial or non-financial item with measurable value (cash, ETF, stock, crypto, property, gold, artwork, private equity, crowdlending, etc.). |
| Asset Class | A category grouping similar assets (Equity, Crypto, Real Estate, Precious Metals, Cash, Private Equity...). |
| Provider | An external institution or platform such as a bank, broker, exchange or crowdlending platform. |
| Container | The location where holdings exist (bank account, brokerage account, exchange account, wallet, vault, property, safe deposit box...). |
| Transaction | An immutable financial event that changes one or more holdings. |
| Position | The calculated value of a holding at a specific point in time. |
| Connector | Software component that synchronizes data with a provider. |
| Synchronization | The process of importing or refreshing external information. |
| Recommendation | An explainable suggestion generated from deterministic financial analysis. |
| Goal | A measurable financial objective assigned to a single portfolio. |
| Strategy | The rules that describe how a portfolio should evolve to achieve its goal. |
| Dashboard | A configurable view composed of widgets. |
| Widget | A reusable visualization component displayed on a dashboard. |
| Financial Engine | The deterministic engine responsible for all financial calculations. |
| AI Assistant | The component that explains information and assists the user. It never replaces the Financial Engine. |

---

# Reserved Terms

The following terms must not be used as synonyms:

| Preferred | Avoid |
|-----------|-------|
| Workspace | Account (top-level meaning) |
| Portfolio | Investment Account |
| Holding | Balance |
| Provider | Platform, Institution (when referring to integrations) |
| Connector | Integration |
| Goal | Target |
| Recommendation | Advice |

---

# Future Concepts

The following concepts are expected to be defined later:

- Tax Profile
- Risk Profile
- Tax Engine
- Knowledge Engine
- Notification
- Alert
- Automation
- Workflow

---

# Change Rules

New business concepts must be added here before they are introduced into:

- documentation;
- architecture;
- database schema;
- APIs;
- source code.

---

# Change Log

| Version | Description |
|---------|-------------|
| 0.1 | Initial ubiquitous language |
