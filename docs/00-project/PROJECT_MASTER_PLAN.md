# PROJECT_MASTER_PLAN

Document ID: PRJ-MASTER-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Depends On

* PROJECT_CONSTITUTION.md
* PROJECT_PHILOSOPHY.md
* PRODUCT_PRINCIPLES.md
* PRODUCT_VISION.md

---

# 1. Purpose

The Project Master Plan defines the governance, roadmap and documentation strategy for the Wealth Platform.

It is the primary navigation document for the project and explains what must be produced, in which order, and why.

The objective is to ensure that the project evolves through well-defined phases, where each phase produces stable deliverables that become the foundation for the following phases.

---

# 2. Objectives

This document ensures that:

* documentation is produced in a logical order;
* dependencies between documents are explicit;
* the project remains coherent as it grows;
* AI and human contributors share the same understanding of the project;
* implementation work starts only after the corresponding documentation has been accepted.

---

# 3. Documentation Structure

```text
docs/
├── 00-project/
├── 01-domain/
├── 02-requirements/
├── 03-architecture/
├── 04-data/
├── 05-security/
├── 06-ai/
├── 07-testing/
├── 08-devops/
├── 09-operations/
└── 10-product/
```

The documentation is organized from business concepts towards implementation.

Each directory represents a progressively more detailed level of specification.

---

# 4. Project Phases

| Phase             | Goal                                             | Status      |
| ----------------- | ------------------------------------------------ | ----------- |
| Foundation        | Define product identity and governance           | ✅ Completed |
| Conceptual Domain | Define the business domain and core capabilities | ✅ Completed |
| Logical Domain    | Define logical domain models and relationships   | Planned     |
| Requirements      | Define functional behaviour                      | Planned     |
| Architecture      | Design the software architecture                 | Planned     |
| Data              | Define the persistence model                     | Planned     |
| AI                | Define AI capabilities                           | Planned     |
| UX                | Define user experience                           | Planned     |
| Security          | Define security architecture                     | Planned     |
| Testing           | Validate quality                                 | Planned     |
| Delivery          | Deploy and operate                               | Planned     |

---

# 5. Documentation Lifecycle

Every document follows the same lifecycle:

1. Draft
2. Founder Review
3. Architecture Review
4. Accepted
5. Versioned
6. Implemented

Only Accepted documents may be used as authoritative references for subsequent documents.

---

# 6. Git Strategy

* One coherent business change = one commit.
* Major milestones may receive Git tags.
* The repository is the single source of truth.
* Accepted documents should always be committed before implementation begins.

---

# 7. Definition of Done

A document is complete when:

* technically consistent;
* aligned with previous architectural decisions;
* reviewed by the Founder;
* reviewed by the Chief Software Architect;
* status updated to Accepted;
* committed to the repository.

---

# 8. Current Project Status

## Completed

* Project Governance
* Product Vision
* Product Principles
* Ubiquitous Language
* Wealth Model
* Business Capabilities
* Asset Management
* Transaction Management
* Portfolio Management
* Financial Planning

These documents constitute the **Domain Model v1.0** of the Wealth Platform.

## Current Focus

Logical Domain Design.

---

# 9. Future Deliverables

The repository is expected to contain more than 100 documents covering:

* Business Domain
* Requirements
* Architecture
* Data
* AI
* Security
* Testing
* Operations
* Product
* DevOps

The next major milestone is the completion of the Logical Domain documentation.

---

# 10. Living Document

This document evolves during the project.

Changes to project phases, documentation strategy or governance must be reflected here before implementation work begins.

---

# 11. Change Log

| Version | Date            | Description                                                                                                                                              |
| ------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0.1     | Initial version | First official master plan                                                                                                                               |
| 1.0     | 2026-06         | Updated after completion of the Conceptual Domain. Added project status, revised roadmap and aligned governance with the accepted documentation process. |
