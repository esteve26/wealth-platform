# BOUNDED_CONTEXTS

Document ID: ARCH-BC-001
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* APPLICATION_ARCHITECTURE.md
* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* BUSINESS_CAPABILITIES.md

---

# 1. Purpose

This document defines the bounded contexts of the Wealth Platform.

A bounded context is a logical boundary where a specific business model, terminology and set of responsibilities remain consistent.

Bounded contexts are used to organize the application architecture and guide future implementation.

---

# 2. Context Map

The Wealth Platform is divided into the following bounded contexts:

| Bounded Context          | Main Responsibility                                    |
| ------------------------ | ------------------------------------------------------ |
| Workspace Context        | Tenant boundary and workspace configuration            |
| Identity Context         | Authentication, authorization and memberships          |
| Organization Context     | Organizations, advisors and client relationships       |
| Provider Context         | Providers, connectors and containers                   |
| Asset Context            | Canonical asset catalog                                |
| Transaction Context      | Immutable financial events                             |
| Financial Engine Context | Deterministic calculations and derived financial state |
| Portfolio Context        | Investment grouping and portfolio structure            |
| Planning Context         | Financial plans, goals and planning assumptions        |
| Intelligence Context     | Insights, recommendations and alerts                   |
| Dashboard Context        | Dashboards, widgets and reports                        |
| Document Context         | Business documents and metadata                        |
| Notification Context     | User notifications                                     |
| Audit Context            | Audit records and compliance traceability              |
| Tax Context              | Tax profiles, lots and tax reporting                   |
| AI Assistant Context     | Conversational explanations and summaries              |

---

# 3. Core Processing Flow

```text
Provider Context
        │
        ▼
Transaction Context
        │
        ▼
Financial Engine Context
        │
        ▼
Portfolio Context
        │
        ▼
Planning Context
        │
        ▼
Intelligence Context
        │
        ▼
Dashboard / AI Assistant
```

---

# 4. Context Ownership

## Workspace Context

Owns:

* Workspace
* WorkspaceConfiguration
* WorkspaceMembership context

Provides workspace boundaries to all other contexts.

---

## Identity Context

Owns:

* Identity
* Role
* Permission
* Authorization decisions

Provides identity and access control to all contexts.

---

## Organization Context

Owns:

* Organization
* OrganizationMember
* ClientRelationship
* AdvisorAssignment

---

## Provider Context

Owns:

* Provider
* Connector
* Container
* Synchronization

Imports external evidence but never owns financial truth.

---

## Asset Context

Owns:

* Asset
* AssetClassification
* MarketReference

Provides canonical asset definitions.

---

## Transaction Context

Owns:

* Transaction
* TransactionLine
* TransactionReference

Transactions are immutable and represent financial history.

---

## Financial Engine Context

Owns:

* Position
* Holding
* Valuation
* Performance
* Allocation
* Progress

This context is the only source of deterministic financial calculations.

---

## Portfolio Context

Owns:

* Portfolio
* PortfolioPosition assignment
* PortfolioStrategy
* TargetAllocation

Portfolio structure does not include financial calculations.

---

## Planning Context

Owns:

* FinancialPlan
* FinancialGoal
* PlanningAssumption

Planning defines intent and objectives.

---

## Intelligence Context

Owns:

* Insight
* Recommendation
* Opportunity
* RiskAssessment

Consumes Financial Engine outputs and produces explainable intelligence.

---

## Dashboard Context

Owns:

* Dashboard
* Widget
* Report

Displays information but never calculates financial truth.

---

## Document Context

Owns:

* Document
* DocumentMetadata
* DocumentVersion

---

## Notification Context

Owns:

* Notification
* NotificationDeliveryStatus

---

## Audit Context

Owns:

* AuditRecord
* ComplianceEvent
* AuditTrail

---

## Tax Context

Owns:

* TaxProfile
* TaxLot
* FiscalEvent
* TaxReport

---

## AI Assistant Context

Owns:

* AIConversation
* Explanation
* Summary

AI never owns financial truth.

---

# 5. Dependency Rules

The following dependency rules apply:

1. Contexts may read information from upstream contexts through explicit interfaces.
2. Contexts may not directly modify aggregates owned by another context.
3. Cross-context changes occur through commands, domain events or application services.
4. Financial calculations may only be requested from the Financial Engine Context.
5. AI may retrieve and explain information but may not bypass context boundaries.
6. Audit may observe all sensitive events but may not modify business state.

---

# 6. Allowed Collaboration Patterns

## Direct Query

Used when one context needs read-only information from another context.

Example:

Portfolio Context queries Position snapshots from Financial Engine Context.

---

## Command Delegation

Used when a context needs another context to perform an owned operation.

Example:

Provider Context requests Transaction Context to import Transactions.

---

## Domain Event Subscription

Used when a context reacts to a completed business fact.

Example:

Financial Engine Context reacts to TransactionProcessed.

---

## Integration Event

Used for external or asynchronous processing.

Example:

Notification Context receives NotificationRequested.

---

# 7. Forbidden Patterns

The following patterns are forbidden:

* One context directly updates another context's aggregate.
* Dashboard performs financial calculations.
* AI Assistant creates financial values.
* Provider data overwrites Financial Engine calculations.
* Portfolio stores performance as owned business state.
* Planning calculates progress directly.
* Transactions are edited after processing.

---

# 8. Context Boundary Decisions

## CBD-001 — Position belongs to Financial Engine Context

Position is a persistent derived state calculated from Transactions.

It is not manually edited and is not owned by Transaction Context.

---

## CBD-002 — Holding belongs to Financial Engine Context

Holding is an aggregation derived from Positions.

It is never manually modified.

---

## CBD-003 — Portfolio belongs to Portfolio Context

Portfolio owns structure and strategy but not valuation or performance.

---

## CBD-004 — Financial Plan belongs to Planning Context

Financial Plan owns goals and planning assumptions but not progress calculation.

---

## CBD-005 — Provider Context owns Container

Container represents the custody location exposed by a Provider.

A Container may hold Positions, but it does not own them.

---

# 9. Implementation Guidance

Each bounded context should eventually map to a clear application module.

A bounded context may become:

* a module in a modular monolith;
* a service boundary in a distributed architecture;
* a package boundary in the codebase.

The first implementation should favor a modular monolith unless a strong operational reason requires service separation.

Bounded contexts must be explicit in the code structure even if they are deployed together.

---

# 10. Acceptance Criteria

This document is complete when:

* every bounded context is identified;
* every context has clear ownership;
* dependency rules are explicit;
* forbidden patterns are documented;
* implementation guidance is technology-neutral.

---

# 11. Change Log

| Version | Description                           |
| ------- | ------------------------------------- |
| 0.1     | Initial bounded context architecture. |
