# AI_IMPLEMENTATION_GUIDE

Document ID: AI-IMP-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Depends On

* PROJECT_CONSTITUTION.md
* DOCUMENTATION_CONVENTIONS.md
* IMPLEMENTATION_TRACEABILITY.md
* OPERATION_CONTRACT_SPECIFICATION.md
* QUALITY_STRATEGY.md

---

# 1. Purpose

This document defines the mandatory implementation workflow for AI coding agents.

Its objective is to ensure that every implementation:

* preserves the architecture;
* remains traceable;
* is deterministic;
* produces consistent code;
* generates tests and documentation automatically.

This guide is implementation-methodology independent and transport independent.

---

# 2. AI First Principles

Every AI coding agent must follow these principles.

## AI-001 — Documentation is the Source of Truth

The implementation follows the documentation.

The implementation must never redefine business rules.

---

## AI-002 — Never Invent Architecture

If architectural information is missing:

* stop;
* report the missing information;
* request clarification.

Never invent:

* new Aggregates;
* new Operations;
* new persistence strategies;
* new architectural layers.

---

## AI-003 — Preserve Existing Architecture

New code must fit the existing architecture.

The architecture must never be modified implicitly.

---

## AI-004 — Small Deterministic Changes

Implement one Operation Contract at a time.

Avoid unrelated refactoring.

---

# 3. Reading Order

Before implementing any feature, the AI must read the documentation in the following order.

1. PROJECT_CONSTITUTION.md
2. DOCUMENTATION_CONVENTIONS.md
3. IMPLEMENTATION_TRACEABILITY.md
4. Functional Specification
5. Ubiquitous Language
6. DOMAIN_ARCHITECTURE.md
7. AGGREGATE_CATALOG.md
8. APPLICATION_SERVICES.md
9. OPERATION_CONTRACT_SPECIFICATION.md
10. Operation Contract
11. ENTITY_MAPPING.md
12. QUALITY_STRATEGY.md

No implementation may begin before this context is available.

---

# 4. Implementation Workflow

For every Operation Contract the AI shall execute the following workflow.

## Phase 1 — Understand

Identify:

* business purpose;
* owning Aggregate;
* owning Application Service;
* business inputs;
* expected outputs;
* business rules.

---

## Phase 2 — Validate

Verify:

* traceability;
* ownership;
* architecture consistency;
* persistence strategy.

---

## Phase 3 — Implement Domain

Generate only when required:

* Aggregate changes;
* Value Objects;
* Domain Events;
* Domain Services.

---

## Phase 4 — Implement Application

Generate:

* Command or Query;
* Validator;
* Handler;
* Application Service methods.

---

## Phase 5 — Implement Persistence

Generate:

* Repository implementation;
* Entity mapping;
* Persistence configuration;
* Migration (if required).

---

## Phase 6 — Implement Delivery

Generate transport adapters.

Examples:

* REST controller;
* MCP tool;
* CLI command;
* Scheduled job.

Transport adapters must remain thin.

---

## Phase 7 — Testing

Generate:

* Unit Tests;
* Integration Tests;
* Contract Tests;
* UI Tests (when applicable).

---

## Phase 8 — Documentation

Update:

* traceability;
* operation documentation;
* changelog;
* architectural references if required.

---

# 5. Output Expectations

Every implementation must generate:

* production code;
* automated tests;
* documentation updates;
* migrations when required;
* buildable solution.

Partial implementations are not acceptable unless explicitly requested.

---

# 6. Architectural Constraints

AI agents must never:

* bypass Application Services;
* bypass Operation Contracts;
* place business rules inside controllers;
* place business rules inside repositories;
* calculate financial values outside the Financial Engine;
* violate Aggregate ownership.

---

# 7. Code Generation Rules

Generated code must:

* compile;
* follow repository conventions;
* preserve naming conventions;
* follow dependency rules;
* include XML documentation where applicable.

Generated code must never include placeholder implementations unless explicitly requested.

---

# 8. Testing Rules

Every implemented Operation must include:

* positive path tests;
* validation tests;
* authorization tests;
* persistence tests;
* integration tests.

When applicable:

* concurrency tests;
* idempotency tests;
* Financial Engine verification tests.

---

# 9. Quality Gates

Before considering an Operation complete, verify:

* documentation is satisfied;
* build succeeds;
* tests pass;
* architecture rules are preserved;
* traceability is complete.

---

# 10. Missing Information Protocol

If the documentation is insufficient, the AI must:

1. identify the missing information;
2. explain why implementation cannot continue safely;
3. propose documentation changes;
4. wait for approval.

The AI must not guess.

---

# 11. Change Policy

The AI may:

* add implementation;
* improve implementation;
* generate tests;
* improve documentation.

The AI may not:

* redefine architecture;
* rename Aggregates;
* change ownership;
* modify persistence strategy;
* introduce undocumented functionality.

---

# 12. Definition of Done

An Operation is complete only when:

* implementation exists;
* tests pass;
* documentation is updated;
* traceability is complete;
* architecture validation succeeds.

---

# 13. AI Success Criteria

The objective of an AI coding agent is not to maximize generated code.

The objective is to maximize architectural correctness, maintainability and traceability while minimizing undocumented decisions.

---

# 14. Acceptance Criteria

This guide is complete when:

* the implementation workflow is explicit;
* architectural responsibilities are clear;
* forbidden behaviors are documented;
* quality gates are defined;
* missing-information handling is deterministic.

---

# 15. Change Log

| Version | Description                            |
| ------- | -------------------------------------- |
| 1.0     | Initial AI implementation methodology. |
