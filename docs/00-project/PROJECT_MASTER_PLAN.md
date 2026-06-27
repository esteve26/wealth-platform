# PROJECT_MASTER_PLAN

Document ID: PRJ-MASTER-001
Version: 0.1
Status: Accepted
Owner: Product & Architecture

## Depends On

- PROJECT_CONSTITUTION.md
- PROJECT_PHILOSOPHY.md
- PRODUCT_PRINCIPLES.md
- PRODUCT_VISION.md

---

# 1. Purpose

The Project Master Plan defines the governance, roadmap and documentation strategy for the Wealth Platform.

It is the primary navigation document for the project and explains what must be produced, in which order, and why.

---

# 2. Objectives

This document ensures that:

- documentation is produced in a logical order;
- dependencies between documents are explicit;
- the project remains coherent as it grows;
- AI and human contributors share the same understanding of the project.

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

---

# 4. Project Phases

| Phase | Goal | Status |
|------|------|--------|
| Foundation | Define product identity | In Progress |
| Domain | Define business domain | Planned |
| Requirements | Define product behaviour | Planned |
| Architecture | Design the software | Planned |
| Data | Define information model | Planned |
| AI | Define AI capabilities | Planned |
| UX | Define user experience | Planned |
| Security | Protect the platform | Planned |
| Testing | Validate quality | Planned |
| Delivery | Deploy and operate | Planned |

---

# 5. Documentation Lifecycle

Every document follows the same lifecycle:

1. Draft
2. Founder Review
3. Architecture Review
4. Accepted
5. Versioned
6. Implemented

Only Accepted documents may be referenced by subsequent documents.

---

# 6. Git Strategy

- One accepted document = one commit.
- Major milestones may receive Git tags.
- The repository is the single source of truth.

---

# 7. Definition of Done

A document is complete when:

- technically consistent;
- aligned with previous decisions;
- approved by the Founder;
- status updated to Accepted.

---

# 8. Future Deliverables

The repository is expected to contain more than 100 documents covering:

- Business Domain
- Requirements
- Architecture
- Data
- AI
- Security
- Testing
- Operations
- Product
- DevOps

---

# 9. Living Document

This document evolves during the project.

Any structural change to the project should be reflected here before implementation work begins.

---

# 10. Change Log

| Version | Date | Description |
|---------|------|-------------|
| 0.1 | Initial version | First official master plan |
