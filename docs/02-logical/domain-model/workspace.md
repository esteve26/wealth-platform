# WORKSPACE

Document ID: LOG-DM-001
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* domain-model/README.md
* WORKSPACE_MANAGEMENT Capability

---

# 1. Purpose

Workspace is the root business boundary of the Wealth Platform.

Every business object exists within exactly one Workspace.

The Workspace provides ownership, isolation, configuration and execution context for all business operations.

---

# 2. Primary Business Entity

## Workspace

The Workspace is the primary business entity responsible for grouping and isolating all business information belonging to a single logical environment.

A Workspace represents a complete financial universe.

Every aggregate belongs to exactly one Workspace.

The Workspace is the root ownership boundary of the domain.

---

# 3. Supporting Entities

## WorkspaceMember

Represents the participation of an Identity within a Workspace.

Responsibilities:

* membership
* role assignment
* permission inheritance
* status

---

## WorkspaceConfiguration

Represents business configuration affecting every aggregate inside the Workspace.

Examples:

* Base Currency
* Locale
* Time Zone
* Historical Retention Policy
* Valuation Preferences

---

# 4. Value Objects

## WorkspaceId

Unique immutable identifier.

---

## WorkspaceName

Human-readable name.

---

## Currency

Default financial currency.

---

## Locale

Language and regional configuration.

---

## TimeZone

Execution time zone.

---

# 5. Relationships

Workspace owns:

* Assets
* Transactions
* Positions
* Portfolios
* Financial Plans
* Documents
* Notifications
* Configuration

Workspace references:

* Organization
* Identities
* Providers

Workspace never owns external Providers.

---

# 6. Business Invariants

## WI-001

Every business object belongs to exactly one Workspace.

---

## WI-002

Workspace ownership never changes implicitly.

---

## WI-003

Business operations always execute inside one Workspace.

---

## WI-004

Workspace isolation is absolute.

Business objects from different Workspaces never interact directly.

---

## WI-005

Deleting a Workspace never silently destroys historical financial information.

---

# 7. Lifecycle

```text
Created
    │
    ▼
Active
    │
    ├──────────────┐
    ▼              │
Suspended          │
    │              │
    ▼              │
Active ◄───────────┘
    │
    ▼
Archived
```

Rules:

* Archived Workspaces become read-only.
* Archived Workspaces preserve historical information.
* Archived Workspaces cannot execute new business operations.

---

# 8. Domain Events

Published:

* WorkspaceCreated
* WorkspaceActivated
* WorkspaceSuspended
* WorkspaceArchived
* WorkspaceConfigurationChanged
* WorkspaceMemberAdded
* WorkspaceMemberRemoved

Consumed:

* OrganizationCreated
* IdentityInvited

---

# 9. Business Operations

Lifecycle

* Create Workspace
* Activate Workspace
* Suspend Workspace
* Archive Workspace

Membership

* Add Member
* Remove Member
* Change Member Role

Configuration

* Update Configuration
* Change Base Currency
* Change Locale
* Change Time Zone

---

# 10. Ownership Rules

Workspace owns:

* Workspace lifecycle
* Workspace configuration
* Workspace membership

Workspace never owns:

* Identity
* Organization
* Provider
* Asset
* Transaction
* Portfolio
* Financial Plan

Workspace only provides the ownership boundary for those aggregates.

---

# 11. Implementation Constraints

The Workspace aggregate must remain lightweight.

Business data belongs to its own aggregates.

The Workspace must never become a "God Aggregate" containing business logic from other domains.

---

# 12. Acceptance Criteria

The Workspace model is complete when:

* ownership boundaries are explicit;
* lifecycle is defined;
* invariants are documented;
* relationships are unambiguous;
* aggregate responsibilities remain limited.

---

# 13. Open Questions

None.

---

# 14. Change Log

| Version | Description                             |
| ------- | --------------------------------------- |
| 0.1     | Initial Workspace aggregate definition. |
