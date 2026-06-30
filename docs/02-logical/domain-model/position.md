# POSITION

Document ID: LOG-DM-008
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* domain-model/README.md
* TRANSACTION
* ASSET
* CONTAINER
* FINANCIAL_ENGINE Capability

---

# 1. Purpose

The Position aggregate represents the current deterministic state of ownership of one Asset inside one Container.

A Position is not manually created or edited.

It is a persistent snapshot produced and maintained exclusively by the Financial Engine from the immutable Transaction history.

The Position aggregate exists to provide efficient access to the current financial state without replaying the complete Transaction history.

---

# 2. Aggregate Ownership

**Owning Capability:** Financial Engine

The Financial Engine is the only capability allowed to create, update or recalculate Positions.

No user interaction modifies a Position directly.

---

# 3. Primary Business Entity

## Position

A Position represents the current ownership state of one Asset within one Container.

A Position is uniquely identified by the combination of:

* Workspace
* Container
* Asset

A Position may exist even when its quantity is zero if historical traceability requires it.

---

# 4. Supporting Entities

## PositionSnapshot

Represents the calculated financial state at a specific point in time.

Contains values such as:

* Quantity
* Average Cost
* Market Value
* Unrealized Gain
* Realized Gain
* Last Recalculation Timestamp

---

## PositionValuation

Represents the latest valuation produced by the Financial Engine.

Valuations are deterministic and reproducible.

---

# 5. Value Objects

## PositionId

Globally unique identifier.

---

## Quantity

Current owned quantity.

---

## AverageCost

Weighted average acquisition cost.

---

## Money

Monetary value.

---

## PositionStatus

Possible values:

* Open
* Closed

---

# 6. Relationships

Position belongs to:

* Workspace
* Container

Position references:

* Asset

Position is produced from:

* Transactions

Position contributes to:

* Portfolio

Position never owns:

* Transactions
* Portfolio
* Financial Plan

---

# 7. Business Invariants

## PSI-001

A Position is always derived from Transactions.

---

## PSI-002

Users cannot manually modify a Position.

---

## PSI-003

At most one active Position exists for the same Workspace, Container and Asset.

---

## PSI-004

Recalculating a Position with the same Transaction history always produces the same result.

---

## PSI-005

Every Position belongs to exactly one Container.

---

## PSI-006

Every Position belongs to exactly one Workspace.

---

# 8. Lifecycle

```text
Calculated
     │
     ▼
Updated
     │
     ▼
Closed
```

Rules:

* Positions are recalculated after relevant Transactions.
* Closed Positions preserve historical information.
* Reopening a Position occurs through new Transactions.

---

# 9. Domain Events

Published:

* PositionCreated
* PositionRecalculated
* PositionClosed
* PositionReopened

Consumed:

* TransactionProcessed
* TransactionCorrected
* AssetUpdated

---

# 10. Business Operations

Executed exclusively by the Financial Engine:

* Create Position
* Recalculate Position
* Close Position
* Reopen Position

No manual business operations exist.

---

# 11. Ownership Rules

Position owns:

* Current calculated state
* Current valuation snapshot
* Position lifecycle

Position never owns:

* Transactions
* Asset definition
* Portfolio allocation
* Financial calculations

The Financial Engine owns every calculation producing Position state.

---

# 12. Implementation Constraints

The Position aggregate is a **persistent derived aggregate**.

Its state is cached for performance but must always be reproducible from the Transaction history.

If inconsistency is detected, the Position must be rebuilt from Transactions.

No external component may update Position state directly.

---

# 13. Acceptance Criteria

The Position aggregate is complete when:

* its derived nature is explicit;
* ownership by the Financial Engine is defined;
* deterministic recalculation is guaranteed;
* invariants prevent manual modification;
* reconstruction from Transactions is always possible.

---

# 14. Open Questions

Future versions may support incremental recalculation strategies for very large Transaction histories.

This optimization must never change deterministic results.

---

# 15. Change Log

| Version | Description                            |
| ------- | -------------------------------------- |
| 0.1     | Initial Position aggregate definition. |
