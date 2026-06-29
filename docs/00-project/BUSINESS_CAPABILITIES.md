# BUSINESS_CAPABILITIES

**Document ID:** PROJ-CAP-001
**Version:** 1.0
**Status:** Accepted
**Owner:** Product & Architecture

---

# Purpose

This document defines the business capabilities of the Wealth Platform.

A business capability represents a stable area of business responsibility.
Capabilities are technology-independent and form the basis for architecture,
implementation and future service boundaries.

---

# Capability Classification

## Core Domain

These capabilities define the unique value of the Wealth Platform.

| Capability | Responsibility |
|------------|----------------|
| Financial Planning | Defines Financial Plans, Purpose, Goals, Strategies, Milestones and planning context. |
| Portfolio Management | Organizes Positions into investment Portfolios that execute Financial Plans. |
| Transaction Management | Records immutable financial events that create or modify Positions. |
| Asset Management | Manages canonical Assets, Asset Classes and reference data. |

---

## Supporting Domain

These capabilities enable the Core Domain.

| Capability | Responsibility |
|------------|----------------|
| Financial Engine | Produces deterministic valuations, performance, allocations and Progress. |
| Provider Integration | Synchronizes data from banks, brokers, exchanges and other providers. |
| Financial Intelligence | Generates explainable insights and recommendations from Financial Engine outputs. |
| Dashboard & Reporting | Presents wealth, planning and portfolio information. |
| AI Assistant | Explains data, answers questions and assists users without generating financial truth. |

---

## Generic Domain

These capabilities support the platform but are not wealth-specific.

| Capability | Responsibility |
|------------|----------------|
| Identity & Access | Authentication, authorization and permissions. |
| Workspace Management | Multi-tenant workspaces and ownership boundaries. |
| Organization Management | Organizations, advisors and client relationships. |
| Administration | Operational administration and platform management. |
| Configuration | User, workspace and platform configuration. |
| Notification | User notifications and alerts. |
| Audit & Compliance | Audit trail and compliance support. |

---

# Capability Relationships

```text
Financial Planning
        │
        ├── uses Portfolio Management
        ├── consumes Financial Engine
        ├── consumes Financial Intelligence
        ├── exposed through Dashboard
        └── explained by AI Assistant

Portfolio Management
        │
        ├── uses Transaction Management
        └── references Asset Management

Transaction Management
        │
        └── creates and modifies Positions

Provider Integration
        │
        └── imports external evidence into the platform

Financial Engine
        │
        └── calculates deterministic financial truth
```

---

# Capability Ownership

| Business Concept | Owning Capability |
|------------------|-------------------|
| Financial Plan | Financial Planning |
| Purpose | Financial Planning |
| Goal | Financial Planning |
| Strategy | Financial Planning |
| Milestone | Financial Planning |
| Progress | Financial Engine (calculation), Financial Planning (presentation) |
| Portfolio | Portfolio Management |
| Position | Transaction Management |
| Holding | Asset Management (derived business view) |
| Asset | Asset Management |
| Asset Class | Asset Management |
| Transaction | Transaction Management |
| Provider | Provider Integration |
| Container | Provider Integration / Workspace Management |

---

# Architectural Principles

- Every business concept has a single owning capability.
- Capabilities own business behaviour, not necessarily every piece of data related to that behaviour.
- Read-only access to concepts owned by another capability is allowed through well-defined business interfaces.
- Capabilities collaborate through business concepts, not database ownership.
- Financial Planning is the primary planning capability.
- Portfolio Management executes planning intent.
- Transactions are immutable.
- Financial Engine is the only source of deterministic financial truth.
- AI never replaces deterministic calculations.

---

# Future Capabilities

Planned capabilities include:

- Tax Management
- Knowledge Engine
- Automation & Workflow
- Document Management
- Client Collaboration

---

# Capability Evolution

The capabilities defined in this document represent the stable business architecture of the Wealth Platform.
Future versions may introduce additional capabilities, but existing responsibilities should only change when a fundamental business decision requires it.
The objective is to maximize long-term architectural stability.

---

# Change Log

| Version | Description |
|---------|-------------|
| 1.0 | Refactored capability map to align with Financial Planning as the primary planning capability and the Wealth Model v1.0. |
