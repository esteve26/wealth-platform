# ORGANIZATION

Document ID: LOG-DM-003
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* domain-model/README.md
* ORGANIZATION_MANAGEMENT Capability
* IDENTITY_ACCESS Capability
* WORKSPACE_MANAGEMENT Capability

---

# 1. Purpose

The Organization aggregate represents a legal entity operating within the Wealth Platform.

Organizations may own Workspaces, manage client Workspaces and assign members to perform business activities on behalf of the Organization.

The Organization aggregate defines the business structure for firms such as family offices, advisory firms, banks, private wealth managers and corporate entities.

---

# 2. Primary Business Entity

## Organization

Organization represents a legal entity using the platform.

An Organization may:

* own one or more Workspaces;
* manage client Workspaces;
* contain Organization Members;
* assign Advisors to client Workspaces.

Organization does not own the financial data inside a Workspace unless it is also the owner of that Workspace.

---

# 3. Supporting Entities

## OrganizationMember

Represents the relationship between an Identity and an Organization.

Responsibilities:

* Organization membership;
* Organization role;
* membership status.

---

## ClientRelationship

Represents a relationship between an Organization and a client Workspace.

Responsibilities:

* client Workspace reference;
* service relationship;
* assigned Advisor;
* relationship status.

---

## AdvisorAssignment

Represents the assignment of one Organization Member to a client Workspace.

Responsibilities:

* Advisor reference;
* client Workspace reference;
* assignment period;
* assignment status.

---

# 4. Value Objects

## OrganizationId

Globally unique identifier.

---

## OrganizationName

Legal or business name of the Organization.

---

## OrganizationType

Possible values:

* Family Office
* Financial Advisory Firm
* Bank
* Private Wealth Manager
* Company
* Other

---

## OrganizationMemberStatus

Possible values:

* Invited
* Active
* Suspended
* Removed

---

## ClientRelationshipStatus

Possible values:

* Active
* Suspended
* Ended

---

# 5. Relationships

Organization references:

* Identity
* Workspace

Organization may manage:

* Client Workspace

Organization never owns:

* Portfolio
* Position
* Transaction
* Financial Plan
* Asset

Those concepts remain owned by their corresponding aggregates inside the Workspace boundary.

---

# 6. Business Invariants

## OI-001

Every Organization has a unique OrganizationId.

---

## OI-002

An Organization may have multiple Organization Members.

---

## OI-003

An Organization may manage multiple client Workspaces.

---

## OI-004

A client Workspace always has a Workspace Owner.

---

## OI-005

An AdvisorAssignment must reference an active Organization Member.

---

## OI-006

Organization permissions are evaluated through Identity & Access.

---

## OI-007

An Organization cannot directly modify business aggregates without valid Workspace authorization.

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

* Archived Organizations are read-only.
* Archived Organizations preserve history.
* Client relationships remain auditable after archival.

---

# 8. Domain Events

Published:

* OrganizationCreated
* OrganizationActivated
* OrganizationSuspended
* OrganizationArchived
* OrganizationMemberAdded
* OrganizationMemberRemoved
* ClientRelationshipCreated
* ClientRelationshipEnded
* AdvisorAssignedToClientWorkspace
* AdvisorRemovedFromClientWorkspace

Consumed:

* IdentityActivated
* WorkspaceCreated
* WorkspaceArchived

---

# 9. Business Operations

Organization lifecycle:

* Create Organization
* Activate Organization
* Suspend Organization
* Archive Organization

Membership:

* Add Organization Member
* Remove Organization Member
* Suspend Organization Member

Client relationships:

* Create Client Relationship
* End Client Relationship
* Assign Advisor
* Remove Advisor

---

# 10. Ownership Rules

Organization owns:

* Organization lifecycle;
* Organization membership;
* client relationships;
* advisor assignments.

Organization never owns:

* Identity;
* Workspace;
* Portfolio;
* Financial Plan;
* Position;
* Transaction;
* Asset.

---

# 11. Implementation Constraints

The Organization aggregate must not become a substitute for Workspace ownership.

All financial operations remain scoped to a Workspace.

Organization-level access always requires authorization through Identity & Access.

---

# 12. Acceptance Criteria

The Organization aggregate is complete when:

* organization ownership boundaries are explicit;
* client Workspace relationships are defined;
* advisor assignment rules are documented;
* lifecycle is defined;
* business invariants are explicit.

---

# 13. Open Questions

None.

---

# 14. Change Log

| Version | Description                                |
| ------- | ------------------------------------------ |
| 0.1     | Initial Organization aggregate definition. |
