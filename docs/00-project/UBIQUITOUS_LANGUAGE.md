# UBIQUITOUS_LANGUAGE

Document ID: DOM-UL-001
Version: 1.0
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

# Authority

This document is the authoritative source for the Wealth Platform business vocabulary.

If another document defines a conflicting meaning for the same business concept, this document takes precedence.

Changes to this document require reviewing all affected domain specifications.

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
| Workspace | Top-level business boundary that contains wealth, financial plans, portfolios, users, providers and settings. A workspace belongs to an individual or an organization. |
| User | A person authenticated in the platform. |
| Organization | A legal entity that manages one or more workspaces or client workspaces. |
| Financial Plan | The primary business planning entity of the Wealth Platform.. A Financial Plan defines why wealth is being managed and how success is measured over time. |
| Purpose | The reason a Financial Plan exists. Describes the intent behind the plan (for example, retirement, education funding or wealth preservation). |
| Goal | A measurable financial objective within a Financial Plan (for example, reach 600,000 EUR by 2045 or build an emergency fund). |
| Strategy | The rules that describe how a Financial Plan intends to achieve its Goals (for example, target return, risk tolerance, asset allocation limits or time horizon). |
| Milestone | A checkpoint within a Financial Plan that marks expected progress toward one or more Goals at a specific point in time. |
| Progress | The measured advancement of a Financial Plan toward its Goals, based on deterministic calculations produced by the Financial Engine. |
| Portfolio | A logical grouping of Positions representing an investment strategy or objective. A Portfolio never performs financial calculations. |
| Position | The current persistent ownership state of an Asset inside a Container. A Position is deterministically derived from the immutable Transaction history by the Financial Engine. Users never modify Positions directly. |
| Holding | An aggregation of Positions for the same Asset. A Holding is a derived business view, not the atomic ownership unit. |
| Asset | A financial or non-financial instrument that exists independently of any Workspace or user. An Asset becomes part of a user's wealth only through a Position. |
| Asset Class | A category grouping similar assets (Equity, Crypto, Real Estate, Precious Metals, Cash, Private Equity...). |
| Provider | An external institution or platform such as a bank, broker, exchange or crowdlending platform. A Provider is never the owner of user wealth. |
| Container | The custody location where wealth is held. Examples include bank accounts, brokerage accounts, crypto wallets, real estate properties and other custody locations. Every Position exists inside exactly one Container. |
| Transaction | An immutable financial event that modifies one or more Positions. |
| Connector | Software component that synchronizes data with a provider. |
| Synchronization | The process of importing or refreshing external information. |
| Recommendation | An explainable suggestion generated from deterministic financial analysis. |
| Dashboard | A configurable view composed of widgets. |
| Widget | A reusable visualization component displayed on a dashboard. |
| Financial Engine | The domain component responsible for every deterministic financial calculation performed by the platform. It produces Position snapshots, portfolio metrics and planning projections from immutable business events. |
| AI Assistant | The component that explains information and assists the user. It never replaces the Financial Engine. |

A **Financial Plan** contains:

- Purpose
- Goals
- Strategies
- Milestones
- Progress
- Linked Portfolios

Portfolios are instruments used to execute or support Financial Plans.

---

# Reserved Terms

The following terms must not be used as synonyms:

| Preferred | Avoid |
|-----------|-------|
| Workspace | Account (top-level meaning) |
| Financial Plan | Financial Profile, Plan Account |
| Portfolio | Investment Account, Broker Account |
| Position | Balance (when referring to atomic owned wealth) |
| Holding | Balance (when referring to aggregated asset exposure) |
| Provider | Platform, Institution (when referring to integrations) |
| Container | Account (when referring generally to where Positions exist) |
| Connector | Integration |
| Goal | Target |
| Recommendation | Advice |
| Financial engine | Calculator |

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
| 0.2 | Aligned Position and Holding definitions with WEALTH_MODEL; added Financial Plan as the primary planning entity; clarified that Transactions modify Positions, Assets are canonical master data, and Portfolios group Positions to support Financial Plans |
