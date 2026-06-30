# PROVIDER

Document ID: LOG-DM-004
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* domain-model/README.md
* PROVIDER_INTEGRATION Capability

---

# 1. Purpose

The Provider aggregate represents an external institution that supplies financial information to the Wealth Platform.

A Provider is the business representation of an external financial organization, independently of the technology used to connect to it.

Examples include banks, brokers, crypto exchanges, pension providers and other financial institutions.

---

# 2. Aggregate Ownership

**Owning Capability:** Provider Integration

The Provider aggregate defines the business identity and lifecycle of external financial institutions.

Synchronization, API communication and connector implementation belong to the Provider Integration capability but remain outside this aggregate.

---

# 3. Primary Business Entity

## Provider

A Provider represents a single external financial institution.

A Provider may expose one or more Containers.

A Provider never owns Assets, Transactions or Positions.

Those concepts belong to their own aggregates.

---

# 4. Supporting Entities

## ProviderConnection

Represents the logical connection between a Workspace and a Provider.

Responsibilities:

* connection status;
* authentication status;
* synchronization status;
* last successful synchronization.

---

## ProviderCredentialReference

Represents a secure reference to credentials managed by the infrastructure.

The aggregate never stores sensitive secrets directly.

---

# 5. Value Objects

## ProviderId

Globally unique identifier.

---

## ProviderName

Business name of the financial institution.

---

## ProviderType

Possible values include:

* Bank
* Broker
* Crypto Exchange
* Pension Provider
* Insurance Company
* Real Estate Platform
* Crowdlending Platform
* Other Financial Institution

---

## ProviderStatus

Possible values:

* Active
* Suspended
* Disabled

---

# 6. Relationships

Provider owns:

* Provider Connections

Provider references:

* Workspace

Provider is referenced by:

* Container

Provider never owns:

* Container contents
* Assets
* Transactions
* Positions
* Portfolios

---

# 7. Business Invariants

## PI-001

Every Provider has a unique ProviderId.

---

## PI-002

A Provider may expose multiple Containers.

---

## PI-003

A Container always belongs to exactly one Provider.

---

## PI-004

A Provider never owns financial assets.

It only identifies the institution responsible for custody.

---

## PI-005

A Provider may be connected to multiple Workspaces independently.

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
Disabled
```

Rules:

* Disabled Providers cannot synchronize.
* Historical financial information remains available.
* Disabling a Provider never removes historical business data.

---

# 9. Domain Events

Published:

* ProviderRegistered
* ProviderActivated
* ProviderSuspended
* ProviderDisabled
* ProviderConnectionEstablished
* ProviderConnectionRemoved
* ProviderSynchronizationSucceeded
* ProviderSynchronizationFailed

Consumed:

* WorkspaceCreated

---

# 10. Business Operations

Provider lifecycle

* Register Provider
* Activate Provider
* Suspend Provider
* Disable Provider

Connections

* Connect Workspace
* Disconnect Workspace
* Validate Connection
* Synchronize Provider

---

# 11. Ownership Rules

Provider owns:

* Provider identity
* Provider lifecycle
* Provider connections

Provider never owns:

* Containers
* Assets
* Transactions
* Positions
* Financial data

---

# 12. Implementation Constraints

The Provider aggregate models the business concept of an external institution.

API protocols, connector implementations, authentication mechanisms and synchronization technologies are infrastructure concerns and must remain outside the aggregate.

---

# 13. Acceptance Criteria

The Provider aggregate is complete when:

* Provider ownership is explicit;
* lifecycle is defined;
* relationships are documented;
* invariants are complete;
* business operations are identified.

---

# 14. Open Questions

None.

---

# 15. Change Log

| Version | Description                            |
| ------- | -------------------------------------- |
| 0.1     | Initial Provider aggregate definition. |
