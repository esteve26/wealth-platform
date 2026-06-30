# IDENTITY

Document ID: LOG-DM-002
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* domain-model/README.md
* IDENTITY_ACCESS Capability

---

# 1. Purpose

The Identity aggregate represents every authenticated actor that can access the Wealth Platform.

Its responsibility is to establish who performs business operations and under which authorization context those operations are executed.

The Identity aggregate owns authentication identity and authorization assignments but never owns business data.

---

# 2. Primary Business Entity

## Identity

Identity represents a unique authenticated actor.

Every business action executed within the platform is performed by exactly one Identity.

An Identity may belong to multiple Organizations and multiple Workspaces.

Identity remains globally unique across the entire platform.

---

# 3. Supporting Entities

## Membership

Represents the relationship between an Identity and a Workspace.

Responsibilities:

* Workspace association
* Membership status
* Assigned Roles
* Effective Permissions

---

## Role Assignment

Associates one or more Roles with a Membership.

Multiple Role Assignments may exist within the same Workspace.

---

## Direct Permission

Represents an explicit permission granted directly to an Identity.

Direct permissions complement Role permissions and may override them according to authorization rules.

---

# 4. Value Objects

## IdentityId

Globally unique identifier.

---

## EmailAddress

Primary business identifier used for authentication.

Must be unique.

---

## DisplayName

Human-readable identity name.

---

## MembershipStatus

Possible values:

* Invited
* Active
* Suspended
* Revoked

---

# 5. Relationships

Identity references:

* Workspace
* Organization
* Role
* Permission

Identity never owns:

* Workspace
* Organization
* Portfolio
* Asset
* Transaction
* Financial Plan

Business ownership always remains within the corresponding aggregate.

---

# 6. Business Invariants

## II-001

Every Identity is globally unique.

---

## II-002

An Identity may belong to multiple Workspaces.

---

## II-003

Authorization is always evaluated within a Workspace context.

---

## II-004

Permissions are granted through Roles or Direct Permissions.

---

## II-005

Every business operation is executed by exactly one authenticated Identity.

---

## II-006

Suspended Identities cannot execute business operations.

---

# 7. Lifecycle

```text
Invited
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
Revoked
```

Rules:

* Revoked Identities permanently lose access.
* Historical business operations remain associated with the original Identity.
* Revocation never removes audit history.

---

# 8. Domain Events

Published:

* IdentityInvited
* IdentityActivated
* IdentitySuspended
* IdentityRevoked
* MembershipAdded
* MembershipRemoved
* RoleAssigned
* RoleRemoved
* DirectPermissionGranted
* DirectPermissionRevoked

Consumed:

* WorkspaceCreated
* OrganizationCreated

---

# 9. Business Operations

Identity

* Invite Identity
* Activate Identity
* Suspend Identity
* Revoke Identity

Membership

* Add Membership
* Remove Membership
* Change Membership Status

Authorization

* Assign Role
* Remove Role
* Grant Direct Permission
* Revoke Direct Permission

---

# 10. Ownership Rules

Identity owns:

* Identity lifecycle
* Workspace Memberships
* Role Assignments
* Direct Permissions

Identity never owns:

* Workspaces
* Organizations
* Business Aggregates
* Financial Information

---

# 11. Implementation Constraints

The Identity aggregate is responsible for business identity.

Authentication technology (OAuth, OpenID Connect, SAML, etc.) is an infrastructure concern and must remain outside the domain model.

Authorization decisions must always be deterministic and auditable.

---

# 12. Acceptance Criteria

The Identity aggregate is complete when:

* ownership boundaries are explicit;
* membership model is defined;
* authorization rules are documented;
* lifecycle is defined;
* business invariants are explicit.

---

# 13. Open Questions

None.

---

# 14. Change Log

| Version | Description                            |
| ------- | -------------------------------------- |
| 0.1     | Initial Identity aggregate definition. |
