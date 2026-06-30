# FS-PORTFOLIO-001 — Create Portfolio

Document ID: FS-PORTFOLIO-001
Version: 1.0
Status: Draft
Owner: Product

## Depends On

* Portfolio Capability
* FUNCTIONAL_SPECIFICATION_GUIDE.md

---

# 1. Purpose

This Functional Specification defines the business capability that allows an authorized user to create a new investment portfolio within an existing workspace.

A portfolio represents an independent investment container that groups assets, transactions, positions and financial metrics.

The creation of a portfolio establishes its business identity but does not contain investment data.

---

# 2. Business Value

Creating portfolios enables users to:

* organize investments independently;
* separate investment strategies;
* manage multiple portfolios within the same workspace;
* establish the foundation for transaction management and financial analysis.

Without portfolios, no investment activity can be recorded.

---

# 3. Actors

## Primary Actor

* Workspace Member

## Supporting Actors

* Authorization Service
* Workspace

---

# 4. Trigger

A workspace member requests the creation of a new portfolio.

---

# 5. Preconditions

The following conditions must already be satisfied.

* The workspace exists.
* The workspace is active.
* The requesting user belongs to the workspace.
* The requesting user has permission to create portfolios.
* The workspace has not exceeded its portfolio limit (if applicable).

---

# 6. Main Business Flow

1. The user initiates portfolio creation.
2. The platform validates authorization.
3. The platform validates business rules.
4. The platform creates a new portfolio.
5. The portfolio becomes available inside the workspace.
6. The user receives confirmation that the portfolio has been created.

---

# 7. Business Rules

## BR-001

Every portfolio belongs to exactly one workspace.

---

## BR-002

Portfolio names must be unique within the same workspace.

Duplicate names are allowed across different workspaces.

---

## BR-003

A portfolio is created in the Active state.

---

## BR-004

A newly created portfolio contains no assets, transactions or positions.

---

## BR-005

A portfolio cannot exist without an owning workspace.

---

## BR-006

Portfolio creation must be auditable.

---

## BR-007

The platform assigns the portfolio identifier.

Users cannot provide it.

---

# 8. Alternative Flows

## AF-001

If the portfolio name already exists inside the workspace, creation is rejected.

---

## AF-002

If the user lacks permission, creation is rejected.

---

## AF-003

If the workspace no longer exists, creation is rejected.

---

# 9. Business Exceptions

Possible business failures include:

* Workspace not found.
* Workspace inactive.
* Duplicate portfolio name.
* Portfolio limit exceeded.
* User not authorized.

Business failures shall not create partial portfolios.

---

# 10. Business Outputs

Successful execution produces:

* One new Portfolio.
* Audit information.
* Confirmation of successful creation.

No financial calculations are performed.

---

# 11. Postconditions

After successful completion:

* the portfolio exists;
* the portfolio belongs to exactly one workspace;
* the portfolio is active;
* the portfolio is visible to authorized workspace members;
* the portfolio contains no investment data.

---

# 12. Success Criteria

The Functional Specification is considered successful when:

* a new portfolio exists;
* all business rules are satisfied;
* no duplicate portfolio exists within the workspace;
* ownership is correctly established;
* audit information is available.

---

# 13. Related Operation Contracts

This Functional Specification is expected to produce the following Operation Contracts.

| Operation        | Description                 |
| ---------------- | --------------------------- |
| OP-PORTFOLIO-001 | Create Portfolio            |
| OP-PORTFOLIO-002 | Validate Portfolio Creation |
| OP-PORTFOLIO-003 | Register Portfolio Audit    |

Future revisions may introduce additional Operation Contracts.

---

# 14. Traceability

| Artifact            | Reference                                            |
| ------------------- | ---------------------------------------------------- |
| Capability          | Portfolio Management                                 |
| Aggregate           | Portfolio                                            |
| Application Service | Portfolio Application Service                        |
| Operation Contracts | OP-PORTFOLIO-001, OP-PORTFOLIO-002, OP-PORTFOLIO-003 |
| Automated Tests     | To be defined                                        |

---

# 15. Out of Scope

The following are explicitly outside the scope of this Functional Specification.

* Recording transactions.
* Creating positions.
* Calculating financial metrics.
* Portfolio performance calculations.
* Portfolio synchronization.
* Asset management.
* Importing investment data.

These capabilities are defined by separate Functional Specifications.

---

# 16. Acceptance Criteria

This Functional Specification is complete when:

* business intent is fully defined;
* business rules are explicit;
* business outputs are unambiguous;
* implementation details are absent;
* traceability is complete.

---

# 17. Change Log

| Version | Description                       |
| ------- | --------------------------------- |
| 1.0     | Initial Functional Specification. |
