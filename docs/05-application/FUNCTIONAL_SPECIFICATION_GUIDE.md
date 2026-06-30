# FUNCTIONAL_SPECIFICATION_GUIDE

Document ID: APP-FS-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Depends On

* PROJECT_CONSTITUTION.md
* PRODUCT_PRINCIPLES.md
* DOCUMENTATION_CONVENTIONS.md
* IMPLEMENTATION_TRACEABILITY.md
* OPERATION_CONTRACT_SPECIFICATION.md

---

# 1. Purpose

This document defines how Functional Specifications shall be written.

A Functional Specification describes **what business capability the platform must provide** and **why it exists**.

It does not describe implementation, architecture or technology.

Functional Specifications are the primary bridge between business requirements and executable Operation Contracts.

---

# 2. Position Within the Methodology

Every feature follows the same lifecycle.

```text
Business Vision
        ↓
Capability
        ↓
Functional Specification
        ↓
Operation Contracts
        ↓
Implementation
```

A Functional Specification is therefore the authoritative description of business behaviour.

---

# 3. Design Principles

## FS-001 — Business First

Functional Specifications describe business behaviour.

They do not describe technical implementation.

---

## FS-002 — Technology Independent

Functional Specifications never reference:

* REST
* HTTP
* Database
* Entity Framework
* PostgreSQL
* .NET
* React
* Next.js

---

## FS-003 — User Intent

Every Functional Specification begins by explaining the business objective from the user's perspective.

---

## FS-004 — Single Business Capability

One Functional Specification describes one coherent business capability.

Multiple independent capabilities require multiple Functional Specifications.

---

## FS-005 — Traceability

Every Functional Specification must be traceable to:

* Capability
* Product Requirement
* Operation Contracts
* Tests

---

# 4. Mandatory Structure

Every Functional Specification shall contain the following sections.

```text
Identity

Purpose

Business Value

Actors

Preconditions

Business Flow

Business Rules

Alternative Flows

Exceptions

Business Outputs

Success Criteria

Operation Contracts

Traceability
```

---

# 5. Identity

Defines:

* Functional Specification ID
* Name
* Owner
* Status
* Version

---

# 6. Purpose

Describes why this capability exists.

The explanation must be understandable by business stakeholders.

---

# 7. Business Value

Explains the expected value.

Examples:

* reduce manual work;
* improve portfolio accuracy;
* automate tax calculations;
* increase data quality.

---

# 8. Actors

Defines who interacts with the capability.

Examples:

* Investor
* Advisor
* Portfolio Manager
* Administrator
* System

Actors are business roles, not technical identities.

---

# 9. Preconditions

Business conditions required before execution.

Examples:

* Portfolio exists.
* Workspace is active.
* User belongs to the workspace.

---

# 10. Business Flow

Describes the normal execution flow.

The flow should be expressed as numbered business steps.

Example:

1. User selects a portfolio.
2. User enters transaction details.
3. Platform validates business rules.
4. Transaction is recorded.
5. Financial metrics are recalculated.
6. User receives confirmation.

No implementation details should appear in this section.

---

# 11. Business Rules

Business Rules define invariant behaviour.

Examples:

* Transactions cannot be modified after reconciliation.
* Portfolio currency cannot change after activation.
* Every asset belongs to one provider.

Business Rules must remain implementation independent.

---

# 12. Alternative Flows

Describe valid variations of the normal flow.

Examples:

* manual import;
* automatic synchronization;
* bulk import.

---

# 13. Exceptions

Describe business failures.

Examples:

* Portfolio not found.
* Unsupported asset.
* Invalid transaction date.

Technical exceptions are documented elsewhere.

---

# 14. Business Outputs

Describe the observable business results.

Examples:

* Portfolio created.
* Transaction imported.
* Financial plan activated.

Business Outputs are independent of transport mechanisms.

---

# 15. Success Criteria

Define measurable completion criteria.

Examples:

* Transaction recorded successfully.
* Portfolio balance updated.
* Import completed without validation errors.

---

# 16. Operation Contracts

Every Functional Specification shall reference one or more Operation Contracts.

Relationship:

```text
Functional Specification

↓

Operation Contract A

Operation Contract B

Operation Contract C
```

One Functional Specification may produce multiple Operation Contracts.

---

# 17. Traceability

Every Functional Specification must reference:

* Capability
* Product Requirement
* Aggregate(s)
* Operation Contract(s)
* Automated Tests

---

# 18. Forbidden Content

Functional Specifications must never contain:

* HTTP methods
* REST endpoints
* JSON payloads
* Database tables
* SQL
* Repository names
* Commands
* Queries
* Handlers
* UI implementation details

These belong to later stages of the methodology.

---

# 19. AI Interpretation

AI coding agents shall interpret Functional Specifications as business intent.

Implementation decisions shall be derived through Operation Contracts.

AI agents must never generate implementation directly from a Functional Specification without passing through the Operation Contract layer.

---

# 20. Acceptance Criteria

A Functional Specification is complete when:

* business intent is explicit;
* business value is defined;
* business rules are complete;
* success criteria are measurable;
* traceability is complete;
* no implementation details are included.

---

# 21. Change Log

| Version | Description                             |
| ------- | --------------------------------------- |
| 1.0     | Initial Functional Specification Guide. |
