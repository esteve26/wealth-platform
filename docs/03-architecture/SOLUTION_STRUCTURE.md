# SOLUTION_STRUCTURE

Document ID: ARCH-SOL-001
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* APPLICATION_ARCHITECTURE.md
* BOUNDED_CONTEXTS.md
* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md

---

# 1. Purpose

This document defines the official source code structure of the Wealth Platform.

Its purpose is to ensure that human developers and AI coding agents implement the system using a consistent, repeatable and predictable architecture.

The structure is optimized for:

* modular monolith implementation;
* Clean Architecture principles;
* Domain-Driven Design boundaries;
* AI-assisted code generation;
* long-term maintainability.

---

# 2. Technology Stack

The official technology stack is:

| Area         | Technology                   |
| ------------ | ---------------------------- |
| Backend      | ASP.NET Core / .NET          |
| Frontend     | Next.js + React + TypeScript |
| Database     | PostgreSQL                   |
| ORM          | Entity Framework Core        |
| Deployment   | Docker                       |
| Architecture | Pragmatic Modular Monolith   |

---

# 3. Repository Structure

The repository must follow this structure:

```text
wealth-platform/
│
├── docs/
│
├── src/
│   │
│   ├── backend/
│   │   └── Wealth.Api/
│   │       ├── Api/
│   │       ├── Modules/
│   │       ├── Shared/
│   │       ├── Infrastructure/
│   │       ├── Program.cs
│   │       └── appsettings.json
│   │
│   └── frontend/
│       ├── app/
│       ├── modules/
│       ├── shared/
│       ├── infrastructure/
│       ├── package.json
│       └── next.config.js
│
├── tests/
│   ├── backend/
│   └── frontend/
│
├── docker/
│
├── scripts/
│
└── README.md
```

No alternative top-level structure should be introduced without an explicit architectural decision.

---

# 4. Backend Structure

The backend is implemented as a single ASP.NET Core application:

```text
src/backend/Wealth.Api/
```

The backend contains all modules inside:

```text
src/backend/Wealth.Api/Modules/
```

Each module represents one bounded context or closely related context.

---

# 5. Backend Module Structure

Every backend module must follow exactly this structure:

```text
Modules/
└── ModuleName/
    ├── Domain/
    │   ├── Entities/
    │   ├── ValueObjects/
    │   ├── Events/
    │   ├── Services/
    │   └── Rules/
    │
    ├── Application/
    │   ├── Commands/
    │   ├── Queries/
    │   ├── Handlers/
    │   ├── Services/
    │   ├── Validators/
    │   └── DTOs/
    │
    ├── Infrastructure/
    │   ├── Persistence/
    │   ├── Repositories/
    │   ├── External/
    │   └── Configuration/
    │
    └── Presentation/
        ├── Controllers/
        ├── Requests/
        └── Responses/
```

This structure is mandatory for every backend module.

---

# 6. Backend Modules

The initial backend modules are:

```text
Modules/
├── Workspace/
├── Identity/
├── Organization/
├── Provider/
├── Asset/
├── Transaction/
├── FinancialEngine/
├── Portfolio/
├── Planning/
├── Intelligence/
├── Dashboard/
├── Document/
├── Notification/
├── Audit/
├── Tax/
└── AiAssistant/
```

Module names must use PascalCase.

---

# 7. Shared Backend Code

Shared backend code lives in:

```text
src/backend/Wealth.Api/Shared/
```

Allowed shared code includes:

* base entity types;
* value object base classes;
* result types;
* error types;
* domain event abstractions;
* validation abstractions;
* clock abstractions;
* user context abstractions.

Shared code must never contain business rules that belong to a specific module.

---

# 8. Backend Infrastructure

Global infrastructure code lives in:

```text
src/backend/Wealth.Api/Infrastructure/
```

This folder may contain:

* database configuration;
* Entity Framework Core setup;
* authentication provider integration;
* message bus implementation;
* logging;
* caching;
* file storage;
* email delivery;
* external service adapters.

Infrastructure code must not contain domain rules.

---

# 9. Backend API Layer

Global API configuration lives in:

```text
src/backend/Wealth.Api/Api/
```

This folder may contain:

* API versioning;
* middleware;
* filters;
* exception handling;
* OpenAPI configuration;
* authentication setup.

Feature-specific controllers must remain inside the corresponding module.

Example:

```text
Modules/Portfolio/Presentation/Controllers/PortfolioController.cs
```

---

# 10. Frontend Structure

The frontend is implemented using Next.js:

```text
src/frontend/
```

The frontend must follow this structure:

```text
src/frontend/
├── app/
├── modules/
├── shared/
└── infrastructure/
```

---

# 11. Frontend Module Structure

Each frontend module must follow this structure:

```text
modules/
└── module-name/
    ├── components/
    ├── pages/
    ├── hooks/
    ├── services/
    ├── types/
    ├── validation/
    └── index.ts
```

Frontend module names must use kebab-case.

Examples:

```text
modules/portfolio/
modules/financial-planning/
modules/provider-integration/
```

---

# 12. Tests Structure

Tests must mirror the production structure.

```text
tests/
├── backend/
│   └── Modules/
│       └── Portfolio/
│           ├── Domain/
│           ├── Application/
│           └── Integration/
│
└── frontend/
    └── modules/
        └── portfolio/
```

Every module must have tests for:

* domain rules;
* application handlers;
* integration with persistence where applicable;
* frontend behavior where applicable.

---

# 13. Naming Conventions

## Backend

| Element                   | Convention            | Example                       |
| ------------------------- | --------------------- | ----------------------------- |
| Module                    | PascalCase            | Portfolio                     |
| Entity                    | PascalCase            | Portfolio                     |
| Value Object              | PascalCase            | Money                         |
| Command                   | PascalCase + Command  | CreatePortfolioCommand        |
| Query                     | PascalCase + Query    | GetPortfolioQuery             |
| Handler                   | PascalCase + Handler  | CreatePortfolioCommandHandler |
| Repository Interface      | I + Name + Repository | IPortfolioRepository          |
| Repository Implementation | Name + Repository     | PortfolioRepository           |
| Controller                | Name + Controller     | PortfolioController           |
| DTO                       | PascalCase + Dto      | PortfolioDto                  |

---

## Frontend

| Element       | Convention                  | Example              |
| ------------- | --------------------------- | -------------------- |
| Module folder | kebab-case                  | financial-planning   |
| Component     | PascalCase                  | PortfolioSummaryCard |
| Hook          | camelCase prefixed with use | usePortfolio         |
| Type          | PascalCase                  | Portfolio            |
| Service       | camelCase                   | portfolioService     |

---

# 14. Module Dependency Rules

Modules may only depend on:

* Shared abstractions;
* their own internal layers;
* explicit application interfaces from other modules.

Modules must not directly access another module's database tables, repositories or internal entities.

Forbidden:

```text
Portfolio module directly updates Transaction entities.
```

Allowed:

```text
Portfolio module requests Transaction information through an application interface or query model.
```

---

# 15. Layer Dependency Rules

Within each backend module:

```text
Presentation
    ↓
Application
    ↓
Domain

Infrastructure
    ↓
Application / Domain abstractions
```

Rules:

* Domain must not depend on Application.
* Domain must not depend on Infrastructure.
* Application may depend on Domain.
* Presentation may depend on Application.
* Infrastructure implements Application or Domain abstractions.
* Infrastructure must not contain business decisions.

---

# 16. Module Implementation Pattern

Every backend module should expose:

* commands;
* queries;
* handlers;
* validators;
* DTOs;
* controllers;
* repositories where persistence is needed;
* domain events where business facts occur.

A module may omit folders only if they are genuinely unnecessary.

AI agents must not create alternative structures.

---

# 17. Example: Portfolio Module

```text
Modules/
└── Portfolio/
    ├── Domain/
    │   ├── Entities/
    │   │   └── Portfolio.cs
    │   ├── ValueObjects/
    │   │   └── PortfolioName.cs
    │   ├── Events/
    │   │   ├── PortfolioCreated.cs
    │   │   └── PositionAssignedToPortfolio.cs
    │   └── Rules/
    │       └── PortfolioBusinessRules.cs
    │
    ├── Application/
    │   ├── Commands/
    │   │   └── CreatePortfolioCommand.cs
    │   ├── Queries/
    │   │   └── GetPortfolioQuery.cs
    │   ├── Handlers/
    │   │   └── CreatePortfolioCommandHandler.cs
    │   ├── Validators/
    │   │   └── CreatePortfolioCommandValidator.cs
    │   └── DTOs/
    │       └── PortfolioDto.cs
    │
    ├── Infrastructure/
    │   ├── Persistence/
    │   └── Repositories/
    │       └── PortfolioRepository.cs
    │
    └── Presentation/
        ├── Controllers/
        │   └── PortfolioController.cs
        ├── Requests/
        │   └── CreatePortfolioRequest.cs
        └── Responses/
            └── PortfolioResponse.cs
```

---

# 18. AI Code Generation Rules

AI coding agents must follow these rules:

1. Never create files outside the approved structure.
2. Never introduce new architectural layers.
3. Never place business rules in controllers.
4. Never place financial calculations outside FinancialEngine.
5. Never allow one module to modify another module's aggregate directly.
6. Always create tests alongside new business logic.
7. Always follow existing naming conventions.
8. Prefer explicit code over clever abstractions.
9. Keep modules internally consistent.
10. Ask for clarification when a required business rule is missing.

---

# 19. Implementation Contract

## Responsibilities

This document defines:

* repository structure;
* backend module structure;
* frontend module structure;
* test structure;
* dependency rules;
* naming conventions;
* AI code generation rules.

## Allowed Dependencies

Backend modules may depend on:

* Shared abstractions;
* their own Domain layer;
* their own Application layer;
* explicitly published interfaces from other modules.

Frontend modules may depend on:

* shared UI components;
* shared types;
* approved API client services.

## Forbidden Dependencies

The following are forbidden:

* Domain depending on Infrastructure.
* Controllers containing business rules.
* Frontend directly implementing business rules.
* Modules directly modifying other modules' aggregates.
* Financial calculations outside FinancialEngine.
* Infrastructure code deciding business outcomes.

## Expected Output

Any generated implementation must follow this structure exactly.

---

# 20. AI Implementation Notes

AI agents implementing this repository must:

* use the documented module structure;
* infer module names from bounded contexts;
* place each file in the correct layer;
* generate tests in the mirrored test structure;
* preserve business ownership boundaries;
* keep all financial calculations inside FinancialEngine;
* avoid creating global services unless explicitly required;
* avoid introducing microservices unless explicitly requested.

When uncertain, AI agents must prefer:

* simple modular monolith;
* explicit folder placement;
* small focused classes;
* deterministic behavior;
* business-rule preservation.

---

# 21. Acceptance Criteria

This document is complete when:

* the backend structure is unambiguous;
* the frontend structure is unambiguous;
* module boundaries are clear;
* dependency rules are explicit;
* AI code generation rules are documented;
* implementation contracts are defined.

---

# 22. Change Log

| Version | Description                            |
| ------- | -------------------------------------- |
| 0.1     | Initial solution structure definition. |
