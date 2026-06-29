# ORGANIZATION_MANAGEMENT

Document ID: CAP-ORG-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Depends On

* PROJECT_CONSTITUTION.md
* PRODUCT_PRINCIPLES.md
* UBIQUITOUS_LANGUAGE.md
* BUSINESS_CAPABILITIES.md

---

# 1. Purpose

Organization Management manages legal entities that operate within the Wealth Platform.

Organizations may own Workspaces, manage client Workspaces and delegate responsibilities to their members.

---

# 2. Responsibilities

Responsible for:

* organization lifecycle;
* organization hierarchy;
* client relationships;
* workspace ownership;
* advisor assignment;
* organization settings.

Not responsible for:

* authentication;
* portfolio management;
* financial calculations.

---

# 3. Business Concepts

## Organization

A legal entity using the platform.

---

## Client Workspace

A Workspace managed on behalf of another owner.

---

## Organization Member

An Identity belonging to an Organization.

---

## Advisor

A member authorized to manage one or more client Workspaces.

---

# 4. Business Operations

* Create Organization
* Update Organization
* Archive Organization
* Assign Workspace
* Assign Advisor
* Remove Advisor
* Invite Organization Member

---

# 5. Business Rules

### BR-001

An Organization may own multiple Workspaces.

### BR-002

An Organization may manage Workspaces owned by clients.

### BR-003

Every client Workspace always has an owner.

### BR-004

Advisor permissions are evaluated through Identity & Access.

---

# 6. Capability Interfaces

Consumes:

* Identity
* Workspace

Produces:

* Organization
* Advisor Assignment
* Organization Membership

---

# 7. Dependencies

Consumes:

* Identity & Access
* Workspace Management

Provides:

* Portfolio Management
* Financial Planning
* Dashboard

---

# 8. Security Considerations

* Organization isolation.
* Advisor auditing.
* Membership auditing.

---

# 9. AI Considerations

AI may explain organization structures and permissions.

AI must never assign permissions or advisors.

---

# 10. Acceptance Criteria

* Organization model defined.
* Advisor model defined.
* Client Workspace model documented.

---

# 11. Open Questions

None.

---

# 12. Change Log

| Version | Description           |
| ------- | --------------------- |
| 0.1     | Initial specification |
