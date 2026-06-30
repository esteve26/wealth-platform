# AI Software Factory

Version: 1.0
Status: Accepted

---

# Purpose

The AI Software Factory defines the methodology used to design, implement, validate and evolve the Wealth Platform using AI coding agents.

Unlike the rest of the documentation, which describes **the product**, the AI Software Factory describes **how the product is built**.

The objective is to enable any AI coding agent to implement the platform while preserving:

* business intent;
* architectural consistency;
* code quality;
* traceability;
* maintainability.

The methodology is independent of any specific AI vendor or model.

---

# Architecture

The AI Software Factory is composed of five cooperating engines.

```text
                Knowledge Engine
                        │
                        ▼
                Context Engine
                        │
                        ▼
                Decision Engine
                        │
                        ▼
               Execution Engine
                        │
                        ▼
               Validation Engine
```

Each engine has a single responsibility.

---

# Knowledge Engine

The Knowledge Engine represents the architectural knowledge of the platform.

It includes:

* Project documentation
* Domain documentation
* Architecture documentation
* Data documentation
* Application documentation

Its responsibility is to answer:

> **What is the system?**

---

# Context Engine

The Context Engine assembles the minimum information required to implement one business capability.

Instead of loading the entire documentation set, an AI coding agent receives a focused Context Package.

Typical Context Package:

```text
Project Constitution
        ↓
Functional Specification
        ↓
Capability
        ↓
Aggregate
        ↓
Operation Contract
        ↓
Entity Mapping
        ↓
Quality Strategy
```

Its responsibility is to answer:

> **What information do I need right now?**

---

# Decision Engine

The Decision Engine converts architectural knowledge into deterministic implementation decisions.

Examples:

* Command or Query?
* Aggregate or Domain Service?
* Financial Engine or Aggregate?
* Repository or Projection?

Its responsibility is to answer:

> **How should I implement this?**

---

# Execution Engine

The Execution Engine transforms an Operation Contract into executable software.

Typical outputs include:

* Domain Model
* Commands
* Queries
* Handlers
* Application Services
* Persistence
* Delivery Adapters
* Automated Tests

Its responsibility is to answer:

> **Generate the implementation.**

---

# Validation Engine

The Validation Engine verifies that generated software satisfies the architecture.

Validation includes:

* architecture rules;
* traceability;
* automated tests;
* documentation updates;
* quality gates.

Its responsibility is to answer:

> **Is the implementation correct?**

---

# Guiding Principles

The AI Software Factory follows six principles.

## Documentation First

Documentation is the source of truth.

---

## Architecture Before Code

Architecture is defined before implementation begins.

---

## Deterministic Decisions

AI agents must avoid implicit architectural decisions.

Every architectural decision should be traceable to documentation.

---

## Minimal Context

AI agents receive only the information required for the current task.

Reducing unnecessary context improves consistency and reduces implementation cost.

---

## Single Source of Truth

Every concept is defined once.

Documentation references existing definitions instead of duplicating them.

---

## Human Governance

AI accelerates implementation.

Humans remain responsible for business intent and architectural evolution.

---

# Repository Structure

```text
00-project/
01-domain/
02-logical/
03-architecture/
04-data/
05-application/
06-delivery/
07-security/
08-ai-factory/
```

The first seven sections describe the platform.

The AI Software Factory describes how those sections are consumed by AI coding agents.

---

# AI Workflow

Every implementation follows the same lifecycle.

```text
Understand
        ↓
Assemble Context
        ↓
Take Decisions
        ↓
Generate Code
        ↓
Generate Tests
        ↓
Validate
        ↓
Update Documentation
```

No implementation should bypass any stage.

---

# Responsibilities

## Humans

Responsible for:

* business vision;
* architecture;
* documentation;
* approvals.

## AI Coding Agents

Responsible for:

* implementation;
* testing;
* documentation updates;
* architecture preservation.

---

# Success Criteria

The AI Software Factory is successful when:

* AI agents require no architectural guesswork;
* generated software is consistent;
* architecture remains stable over time;
* documentation and implementation evolve together.

---

# Evolution

The AI Software Factory is intended to evolve independently from the Wealth Platform.

Its principles should remain applicable to other enterprise software systems.

Future projects should be able to reuse this methodology with minimal adaptation.
