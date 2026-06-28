# DEVELOPMENT_WORKFLOW

**Document ID:** PRJ-WORKFLOW-001  
**Version:** 0.1  
**Status:** Draft  
**Owner:** Product & Architecture

---

# 1. Purpose

This document defines how the Wealth Platform is developed using ChatGPT, Cursor, Git and GitHub.

---

# 2. Roles

## Product Owner

Responsible for:

- business decisions;
- priorities;
- approval of documents;
- approval of product behavior.

## Chief Software Architect

Responsible for:

- domain coherence;
- architecture;
- impact analysis;
- detecting inconsistencies;
- defining technical direction.

## Cursor

Responsible for:

- creating and modifying files;
- applying specifications;
- producing diffs;
- assisting implementation.

---

# 3. Standard Workflow

```text
Idea
  ↓
Architecture Discussion
  ↓
Capability Specification
  ↓
Impact Analysis
  ↓
Review
  ↓
Accepted
  ↓
Commit
  ↓
Implementation
  ↓
Tests
  ↓
Release
```

---

# 4. Document Workflow

1. Create Draft.
2. Review functionally.
3. Review architecturally.
4. Perform Impact Analysis.
5. Update affected documents if needed.
6. Mark as Accepted.
7. Commit.

---

# 5. Commit Rules

Use one commit per coherent change.

Examples:

```bash
git commit -m "docs: add financial planning capability"
git commit -m "docs: update domain language for financial plans"
git commit -m "adr: record immutable transactions decision"
```

---

# 6. Impact Analysis

Any document introducing a new concept must identify affected documents.

Example:

```text
New concept: Financial Plan

Affected:
- WEALTH_MODEL.md
- UBIQUITOUS_LANGUAGE.md
- BUSINESS_CAPABILITIES.md
- PORTFOLIO_MANAGEMENT.md
```

---

# 7. Change Log

| Version | Description |
|---------|-------------|
| 0.1 | Initial development workflow |
