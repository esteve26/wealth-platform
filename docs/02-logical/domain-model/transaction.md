# TRANSACTION

Document ID: LOG-DM-007
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* domain-model/README.md
* TRANSACTION_MANAGEMENT Capability
* ASSET
* CONTAINER

---

# 1. Purpose

The Transaction aggregate represents an immutable business event that changes the financial state of a Workspace.

Transactions are the authoritative source of financial history.

Every Position, Holding and Portfolio state can be deterministically reproduced from the complete Transaction history.

---

# 2. Aggregate Ownership

**Owning Capability:** Transaction Management

The Transaction aggregate owns the complete financial event history.

Financial calculations remain the responsibility of the Financial Engine.

---

# 3. Primary Business Entity

## Transaction

A Transaction records a completed financial operation.

Examples include:

* Buy Asset
* Sell Asset
* Dividend
* Interest
* Deposit
* Withdrawal
* Transfer
* Fee
* Tax Payment
* Corporate Action

Transactions are immutable.

---

# 4. Supporting Entities

## TransactionLine

Represents one financial movement within a Transaction.

A Transaction contains one or more TransactionLines.

---

## TransactionReference

Represents references to external providers or imported identifiers.

Examples:

* Bank Transaction ID
* Broker Execution ID
* External Reference

---

# 5. Value Objects

## TransactionId

Globally unique identifier.

---

## TransactionDate

Business effective date.

---

## SettlementDate

Settlement date when applicable.

---

## Money

Monetary value.

---

## Quantity

Asset quantity.

---

## TransactionType

Examples:

* Buy
* Sell
* Deposit
* Withdrawal
* Dividend
* Interest
* Fee
* Transfer
* Tax
* Adjustment

---

# 6. Relationships

Transaction belongs to:

* Workspace
* Container

Transaction references:

* Asset

Transaction produces:

* Position changes

Transaction never owns:

* Position
* Holding
* Portfolio

---

# 7. Business Invariants

## TI-001

Transactions are immutable.

---

## TI-002

Every Transaction belongs to exactly one Workspace.

---

## TI-003

Every Transaction belongs to exactly one Container.

---

## TI-004

Every Transaction references at most one Asset.

Cash transactions may not reference an Asset.

---

## TI-005

Financial history is reproducible exclusively from Transactions.

---

## TI-006

Transactions never perform financial calculations.

---

# 8. Lifecycle

```text
Recorded
    │
    ▼
Validated
    │
    ▼
Processed
```

Rules:

* Processed Transactions are immutable.
* Corrections are performed through compensating Transactions.
* Historical Transactions are never modified or deleted.

---

# 9. Domain Events

Published:

* TransactionRecorded
* TransactionValidated
* TransactionProcessed
* TransactionImported
* TransactionCorrected

Consumed:

* ProviderSynchronizationSucceeded

---

# 10. Business Operations

* Record Transaction
* Import Transaction
* Validate Transaction
* Process Transaction
* Correct Transaction

---

# 11. Ownership Rules

Transaction owns:

* Financial event history
* Transaction metadata
* External references

Transaction never owns:

* Positions
* Holdings
* Portfolio balances
* Financial calculations

---

# 12. Implementation Constraints

The Transaction aggregate is append-only.

Corrections must be represented through additional Transactions rather than modifications of historical records.

The Financial Engine consumes Transactions to calculate deterministic financial state.

---

# 13. Acceptance Criteria

The Transaction aggregate is complete when:

* immutability is guaranteed;
* ownership boundaries are explicit;
* relationships are defined;
* lifecycle is documented;
* deterministic history is preserved.

---

# 14. Open Questions

Future versions may support pending Transactions awaiting settlement.

This capability is intentionally outside the scope of version 1.

---

# 15. Change Log

| Version | Description                               |
| ------- | ----------------------------------------- |
| 0.1     | Initial Transaction aggregate definition. |
