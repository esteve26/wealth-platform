# DOMAIN_ARCHITECTURE

Document ID: LOG-DOM-001
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* PROJECT_CONSTITUTION.md
* PRODUCT_PRINCIPLES.md
* UBIQUITOUS_LANGUAGE.md
* BUSINESS_CAPABILITIES.md
* WEALTH_MODEL.md
* All Capability Specifications

---

# 1. Purpose

This document defines the logical architecture of the Wealth Platform domain.

Its objective is to transform the conceptual business model into an implementation-ready domain architecture while remaining independent from any programming language, framework or persistence technology.

It establishes ownership boundaries, collaboration rules and architectural constraints for all business capabilities.

---

# 2. Architectural Principles

## AP-001 — Business before Technology

The domain architecture represents business concepts.

Technical implementation details are defined in later architectural documents.

---

## AP-002 — Single Ownership

Every business concept has exactly one owning capability.

Other capabilities may consume that concept but never own or modify it.

---

## AP-003 — Deterministic Financial Truth

All financial calculations originate exclusively from the Financial Engine.

No other capability may calculate financial values.

---

## AP-004 — Explainable AI

Artificial Intelligence assists users by explaining deterministic information.

AI never creates financial truth.

---

## AP-005 — Workspace Isolation

Every business object belongs to exactly one Workspace.

No business object may exist outside a Workspace boundary.

---

## AP-006 — Immutable Financial History

Transactions and audit records remain historically reproducible.

Business history is never rewritten.

---

# 3. Core Domain Flow

The Wealth Platform is centered around Positions.

Every business process ultimately creates, modifies, values or explains Positions.

Conceptual flow:

```text
Provider
        │
        ▼
Container
        │
        ▼
Asset
        │
        ▼
Transaction
        │
        ▼
Position
        │
        ▼
Financial Engine
        │
        ▼
Holding
        │
        ▼
Portfolio
        │
        ▼
Financial Plan
        │
        ▼
Financial Intelligence
        │
        ▼
Dashboard / AI Assistant```

This flow represents the primary direction of business processing.

---

# 4. Capability Ownership

| Capability              | Owns                                   |
| ----------------------- | -------------------------------------- |
| Workspace Management    | Workspace                              |
| Identity & Access       | Identity, Role, Permission, Membership |
| Organization Management | Organization                           |
| Provider Integration    | Provider, Connector, Synchronization   |
| Asset Management        | Asset                                  |
| Transaction Management  | Transaction, Position                  |
| Financial Engine        | Holding, Valuation, Financial Metrics  |
| Portfolio Management    | Portfolio                              |
| Financial Planning      | Financial Plan, Goal, Strategy         |
| Financial Intelligence  | Insight, Recommendation                |
| Dashboard & Reporting   | Dashboard, Widget, Report              |
| Notification            | Notification                           |
| Configuration           | Configuration, Preferences             |
| Document Management     | Document                               |
| Audit & Compliance      | Audit Record                           |
| Tax Management          | Tax Profile, Tax Lot                   |
| AI Assistant            | AI Conversation                        |

Every business concept has exactly one owner.

---

# 5. Dependency Rules

Capabilities communicate only through published business interfaces.

The following rules apply:

* Dependencies must always point towards the owner of the required concept.
* Circular dependencies are forbidden.
* Read access is allowed.
* Ownership transfer is forbidden.

Example:

Portfolio Management may consume Positions.

Portfolio Management never owns Positions.

---

# 6. Cross-Capability Collaboration

Business capabilities collaborate through deterministic business information.

Typical collaboration examples:

Provider Integration

↓

Transaction Management

↓

Financial Engine

↓

Financial Intelligence

↓

Dashboard

↓

AI Assistant

Each capability remains responsible only for its own business concepts.

---

# 7. Global Invariants

The following invariants apply to the entire platform.

## GI-001

Every business object belongs to exactly one Workspace.

---

## GI-002

Every Transaction belongs to exactly one Workspace.

---

## GI-003

Every Position belongs to exactly one Workspace.

---

## GI-004

Every Portfolio belongs to exactly one Financial Plan.

---

## GI-005

Every financial value originates from the Financial Engine.

---

## GI-006

AI never produces financial truth.

---

## GI-007

Audit history is immutable.

---

## GI-008

Business ownership never crosses capability boundaries.

---

# 8. Architectural Decisions

## AD-001

The Position is the atomic ownership unit of wealth.

---

## AD-002

Holdings are deterministic aggregations produced by the Financial Engine.

---

## AD-003

Providers are external evidence.

They never own business information.

---

## AD-004

Financial Plans define business objectives.

Portfolios execute investment strategies.

---

## AD-005

Business capabilities communicate through explicit contracts.

Implementation technologies are irrelevant at this level.

---

# 9. Relationship to Subsequent Documents

This document defines the logical architecture.

The following documents refine this architecture:

* DOMAIN_MODEL.md
* DOMAIN_EVENTS.md
* DOMAIN_SERVICES.md
* DOMAIN_RELATIONSHIPS.md

These documents must remain consistent with every architectural decision defined here.

---

# 10. Acceptance Criteria

This document is complete when:

* capability ownership is unambiguous;
* dependency rules are defined;
* global invariants are documented;
* architectural decisions are explicit;
* implementation technologies remain absent.

---

# 11. Open Questions

None.

---

# 12. Change Log

| Version | Description                          |
| ------- | ------------------------------------ |
| 0.1     | Initial logical domain architecture. |
