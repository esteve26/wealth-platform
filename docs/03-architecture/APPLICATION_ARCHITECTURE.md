# APPLICATION ARCHITECTURE

Document ID: ARCH-APP-001
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* domain-model/
* Functional Specifications

---

# 1. Purpose

This document defines the logical application architecture of the Wealth Platform.

Its purpose is to describe how business capabilities are implemented, how application components collaborate and how business operations flow through the system.

The Application Architecture bridges the gap between the Domain Model and the technical implementation.

---

# 2. Architectural Principles

The application follows these principles:

* Domain-Driven Design (DDD)
* Clean Architecture
* CQRS (Command Query Responsibility Segregation)
* Event-Driven Architecture
* Dependency Inversion
* Deterministic Financial Calculations
* API First

Business rules always remain independent from infrastructure.

---

# 3. High-Level Architecture

```text
                User Interface
                       │
                       ▼
                 Application Layer
        ┌────────────────────────────┐
        │ Commands │ Queries │ Events │
        └────────────────────────────┘
                       │
                       ▼
                  Domain Layer
             Aggregates & Services
                       │
                       ▼
              Financial Engine
                       │
                       ▼
                Infrastructure
```

---

# 4. Architectural Layers

## Presentation Layer

Responsible for:

* Web UI
* Mobile UI
* Public APIs
* Authentication entry points

Contains no business rules.

---

## Application Layer

Coordinates business use cases.

Responsibilities:

* Commands
* Queries
* Authorization
* Transactions
* Event publishing
* Orchestration

Contains application logic but no financial calculations.

---

## Domain Layer

Contains the business model.

Includes:

* Aggregates
* Value Objects
* Domain Services
* Business Rules
* Domain Events

This layer is independent of any technology.

---

## Financial Engine

Dedicated domain component responsible for deterministic financial calculations.

Responsibilities include:

* Position calculation
* Portfolio calculation
* Performance calculation
* Goal progress
* Allocation calculation
* Risk metrics

The Financial Engine is the only component allowed to calculate financial state.

---

## Infrastructure Layer

Responsible for technical concerns:

* Database
* External APIs
* Provider connectors
* Message Bus
* Cache
* File Storage
* Authentication providers

Infrastructure never contains business rules.

---

# 5. Request Lifecycle

Every business operation follows the same lifecycle.

```text
User Request
      │
      ▼
Authentication
      │
      ▼
Authorization
      │
      ▼
Command
      │
      ▼
Application Service
      │
      ▼
Aggregate
      │
      ▼
Domain Events
      │
      ▼
Financial Engine (if applicable)
      │
      ▼
Persistence
      │
      ▼
Response
```

---

# 6. Commands

Commands represent business intentions.

Examples:

* CreateWorkspace
* CreatePortfolio
* RecordTransaction
* ImportProvider
* CreateFinancialPlan
* UpdateTargetAllocation

Commands change system state.

---

# 7. Queries

Queries retrieve information.

Examples:

* GetPortfolio
* GetDashboard
* GetTransactions
* GetFinancialPlan
* GetPositionHistory

Queries never modify business state.

---

# 8. Domain Events

Domain Events represent completed business facts.

Examples:

* TransactionRecorded
* PositionRecalculated
* PortfolioCreated
* FinancialGoalCompleted

Domain Events are internal to the business domain.

---

# 9. Integration Events

Integration Events communicate with external systems.

Examples:

* ProviderSynchronizationRequested
* NotificationRequested
* AIAnalysisRequested

Integration Events never modify business rules.

---

# 10. Application Services

Application Services coordinate business use cases.

Examples:

* Workspace Service
* Identity Service
* Provider Service
* Transaction Service
* Portfolio Service
* Financial Planning Service

Application Services orchestrate aggregates but never contain business rules.

---

# 11. Domain Services

Domain Services encapsulate business behaviour that does not naturally belong to a single aggregate.

Examples:

* Financial Engine
* Tax Calculation Service
* Allocation Service
* Rebalancing Service

---

# 12. Dependency Rules

Dependencies always point inward.

```text
Presentation
      │
Application
      │
Domain
      │
Infrastructure
```

The Domain Layer never depends on Infrastructure.

---

# 13. Financial Processing Pipeline

Financial processing follows a deterministic pipeline.

```text
Transaction
      │
      ▼
Validation
      │
      ▼
Financial Engine
      │
      ▼
Position Snapshot
      │
      ▼
Portfolio Metrics
      │
      ▼
Financial Plan Progress
      │
      ▼
Dashboard
```

Every execution with identical inputs must produce identical outputs.

---

# 14. Cross-Cutting Concerns

Applied uniformly across the application:

* Authentication
* Authorization
* Logging
* Auditing
* Validation
* Observability
* Error Handling
* Localization

These concerns are implemented outside the Domain Layer.

---

# 15. Acceptance Criteria

The Application Architecture is complete when:

* architectural layers are defined;
* dependency rules are explicit;
* request lifecycle is documented;
* Commands and Queries are separated;
* financial processing is deterministic.

---

# 16. Change Log

| Version | Description                                  |
| ------- | -------------------------------------------- |
| 0.1     | Initial Application Architecture definition. |
