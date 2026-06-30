# CONTAINER

Document ID: LOG-DM-005
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* domain-model/README.md
* PROVIDER Capability

---

# 1. Purpose

The Container aggregate represents the custody location where wealth is held.

A Container is the business representation of a financial account, wallet, property or any other custody location capable of holding financial or non-financial assets.

Every Position exists inside exactly one Container.

---

# 2. Aggregate Ownership

**Owning Capability:** Provider Integration

The Container aggregate defines the business identity and lifecycle of custody locations.

Synchronization, balance import and connector implementation remain the responsibility of the Provider Integration capability.

---

# 3. Primary Business Entity

## Container

A Container represents one custody location.

Examples include:

* Checking Account
* Savings Account
* Brokerage Account
* Crypto Wallet
* Pension Account
* Mortgage
* Deposit
* Real Estate Property
* Precious Metals Vault

A Container belongs to exactly one Provider.

---

# 4. Supporting Entities

## ContainerOwner

Represents the ownership relationship between a Workspace and a Container.

Responsibilities:

* ownership percentage;
* ownership type;
* effective dates.

---

## ContainerBalance

Represents the latest balance imported from the Provider.

Balances are informational snapshots.

They never replace deterministic Position calculations performed by the Financial Engine.

---

# 5. Value Objects

## ContainerId

Globally unique identifier.

---

## ContainerName

Human-readable name.

---

## ContainerType

Possible values include:

* Checking Account
* Savings Account
* Brokerage Account
* Crypto Wallet
* Pension Account
* Deposit
* Mortgage
* Real Estate Property
* Vault
* Other

---

## ContainerStatus

Possible values:

* Active
* Suspended
* Closed

---

# 6. Relationships

Container belongs to:

* Provider

Container references:

* Workspace

Container contains:

* Positions

Container never owns:

* Assets
* Transactions
* Portfolios
* Financial Plans

---

# 7. Business Invariants

## CI-001

Every Container belongs to exactly one Provider.

---

## CI-002

Every Container belongs to exactly one Workspace.

---

## CI-003

Every Position exists in exactly one Container.

---

## CI-004

A closed Container becomes read-only.

Historical information remains available.

---

## CI-005

Container balances never replace deterministic valuations calculated by the Financial Engine.

---

# 8. Lifecycle

```text
Registered
     │
     ▼
Active
     │
     ├──────────────┐
     ▼              │
Suspended           │
     │              │
     ▼              │
Active ◄────────────┘
     │
     ▼
Closed
```

Rules:

* Closed Containers cannot receive new Transactions.
* Historical Transactions remain immutable.
* Historical Positions remain reproducible.

---

# 9. Domain Events

Published:

* ContainerRegistered
* ContainerActivated
* ContainerSuspended
* ContainerClosed
* ContainerBalanceImported
* ContainerOwnershipChanged

Consumed:

* ProviderSynchronizationSucceeded
* ProviderConnectionEstablished

---

# 10. Business Operations

Lifecycle

* Register Container
* Activate Container
* Suspend Container
* Close Container

Synchronization

* Import Balance
* Refresh Container

Ownership

* Assign Owner
* Update Ownership

---

# 11. Ownership Rules

Container owns:

* Container lifecycle
* Container ownership
* Imported balance snapshots

Container never owns:

* Assets
* Transactions
* Positions
* Financial calculations

---

# 12. Implementation Constraints

A Container represents the custody boundary of wealth.

Financial truth is always derived from Transactions and calculated by the Financial Engine.

Provider balances are informational and may be used for reconciliation, but never as the authoritative source for portfolio valuation.

---

# 13. Acceptance Criteria

The Container aggregate is complete when:

* custody responsibilities are explicit;
* ownership is defined;
* lifecycle is documented;
* invariants are complete;
* relationships are unambiguous.

---

# 14. Open Questions

Future versions may support hierarchical Containers.

Example:

* Bank

  * Checking Account
  * Savings Account

This capability is intentionally out of scope for the initial version.

---

# 15. Change Log

| Version | Description                             |
| ------- | --------------------------------------- |
| 0.1     | Initial Container aggregate definition. |
