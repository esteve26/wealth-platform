# APPLICATION_SERVICES

Document ID: ARCH-AS-001
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* APPLICATION_ARCHITECTURE.md
* BOUNDED_CONTEXTS.md
* SOLUTION_STRUCTURE.md
* QUALITY_STRATEGY.md

---

# 1. Purpose

This document defines the official Application Service architecture of the Wealth Platform.

Application Services coordinate use cases. They do not contain deep business rules, financial calculations or infrastructure concerns.

Their role is to orchestrate commands, queries, aggregates, repositories, domain services and events in a predictable implementation pattern.

---

# 2. Architectural Decisions

## AS-001 — Commands use Command Handlers

All write operations must follow this flow:

```text
Controller
    ↓
CommandHandler
    ↓
ApplicationService
    ↓
Aggregate / Domain Service
    ↓
Repository
    ↓
Domain Events
```

---

## AS-002 — Queries use Query Handlers

All read operations must follow this flow:

```text
Controller
    ↓
QueryHandler
    ↓
Read Model / Repository / Projection
    ↓
Response DTO
```

---

## AS-003 — Application Services orchestrate use cases

Application Services coordinate use cases but do not own business rules.

Business rules belong to Aggregates, Value Objects or Domain Services.

---

## AS-004 — Financial calculations are isolated

Only `FinancialEngineService` may execute deterministic financial calculations.

No other Application Service may calculate Positions, Holdings, Valuations, Performance or Progress.

---

## AS-005 — One aggregate owner

Each aggregate is modified only through its owning Application Service.

Cross-module changes must happen through Commands, Queries or Events.

---

# 3. Application Service Definition

An Application Service is responsible for:

* coordinating a use case;
* loading required aggregates;
* checking authorization context;
* invoking aggregate methods or domain services;
* saving changes;
* publishing events;
* returning application DTOs.

An Application Service is not responsible for:

* HTTP concerns;
* UI behavior;
* infrastructure implementation;
* direct database access;
* financial calculations outside the Financial Engine;
* deep business rules.

---

# 4. Service Catalog

| Application Service      | Main Responsibility                                                  |
| ------------------------ | -------------------------------------------------------------------- |
| WorkspaceService         | Workspace lifecycle and configuration                                |
| IdentityService          | Identity, membership, roles and permissions                          |
| OrganizationService      | Organizations, advisors and client relationships                     |
| ProviderService          | Providers, containers, connectors and synchronization                |
| AssetService             | Canonical asset catalog                                              |
| TransactionService       | Transaction recording, import and validation                         |
| FinancialEngineService   | Position, holding, valuation, performance and progress recalculation |
| PortfolioService         | Portfolio structure, strategy and target allocation                  |
| FinancialPlanningService | Financial plans, goals and planning assumptions                      |
| IntelligenceService      | Insights, recommendations, risks and opportunities                   |
| DashboardService         | Dashboards, widgets and reports                                      |
| DocumentService          | Documents, metadata and versions                                     |
| NotificationService      | Notifications and delivery status                                    |
| AuditService             | Audit records and compliance traceability                            |
| TaxService               | Tax profiles, tax lots and tax reports                               |
| AiAssistantService       | Conversations, explanations and summaries                            |

---

# 5. Write Operation Rules

Every write operation must:

1. Enter through a Command.
2. Be handled by exactly one CommandHandler.
3. Delegate orchestration to one Application Service.
4. Modify only aggregates owned by that service.
5. Persist changes through approved repositories.
6. Publish relevant Domain Events.
7. Generate automated tests.

Forbidden:

* controllers modifying aggregates directly;
* handlers containing business rules;
* services modifying aggregates from another context;
* financial calculations outside FinancialEngineService.

---

# 6. Read Operation Rules

Every read operation must:

1. Enter through a Query.
2. Be handled by exactly one QueryHandler.
3. Return a DTO or read model.
4. Never modify business state.

Queries may use optimized read models, projections or repositories.

Queries must not execute business operations.

---

# 7. Cross-Service Collaboration

Application Services may collaborate only through:

* public application interfaces;
* Commands;
* Queries;
* Domain Events;
* Integration Events.

Direct access to another module's internal entities, repositories or database tables is forbidden.

Example:

Allowed:

```text
PortfolioService queries FinancialEngineService for Position snapshots.
```

Forbidden:

```text
PortfolioService updates Position directly.
```

---

# 8. Service Specifications

## WorkspaceService

Responsible for:

* Create Workspace
* Activate Workspace
* Suspend Workspace
* Archive Workspace
* Update Workspace Configuration
* Add Workspace Member
* Remove Workspace Member

Owns:

* Workspace

Publishes:

* WorkspaceCreated
* WorkspaceConfigurationChanged
* WorkspaceArchived

---

## IdentityService

Responsible for:

* Invite Identity
* Activate Identity
* Suspend Identity
* Revoke Identity
* Assign Role
* Grant Direct Permission
* Revoke Direct Permission

Owns:

* Identity
* Membership
* Role Assignment
* Direct Permission

Publishes:

* IdentityInvited
* IdentityActivated
* RoleAssigned
* DirectPermissionGranted

---

## OrganizationService

Responsible for:

* Create Organization
* Archive Organization
* Add Organization Member
* Create Client Relationship
* Assign Advisor
* Remove Advisor

Owns:

* Organization
* OrganizationMember
* ClientRelationship
* AdvisorAssignment

Publishes:

* OrganizationCreated
* ClientRelationshipCreated
* AdvisorAssignedToClientWorkspace

---

## ProviderService

Responsible for:

* Register Provider
* Connect Provider
* Register Container
* Synchronize Provider
* Import Provider Data
* Refresh Container

Owns:

* Provider
* Container
* Connector
* Synchronization

Publishes:

* ProviderConnected
* ProviderSynchronizationSucceeded
* ProviderSynchronizationFailed
* ContainerRegistered
* ContainerBalanceImported

---

## AssetService

Responsible for:

* Register Asset
* Update Asset
* Reclassify Asset
* Delist Asset

Owns:

* Asset
* AssetClassification
* MarketReference

Publishes:

* AssetCreated
* AssetUpdated
* AssetReclassified
* AssetDelisted

---

## TransactionService

Responsible for:

* Record Transaction
* Import Transaction
* Validate Transaction
* Process Transaction
* Correct Transaction

Owns:

* Transaction
* TransactionLine
* TransactionReference

Publishes:

* TransactionRecorded
* TransactionValidated
* TransactionProcessed
* TransactionCorrected

---

## FinancialEngineService

Responsible for:

* Recalculate Position
* Recalculate Holding
* Calculate Portfolio Metrics
* Calculate Financial Plan Progress
* Calculate Allocation
* Calculate Performance

Owns:

* Position
* Holding
* Valuation
* Performance
* Allocation
* Progress

Consumes:

* TransactionProcessed
* TransactionCorrected
* AssetUpdated
* ExchangeRateUpdated

Publishes:

* PositionRecalculated
* HoldingRecalculated
* PortfolioMetricsCalculated
* FinancialPlanProgressCalculated

---

## PortfolioService

Responsible for:

* Create Portfolio
* Activate Portfolio
* Archive Portfolio
* Assign Position
* Remove Position
* Change Portfolio Strategy
* Update Target Allocation

Owns:

* Portfolio
* PortfolioPosition assignment
* PortfolioStrategy
* TargetAllocation

Publishes:

* PortfolioCreated
* PositionAssignedToPortfolio
* PortfolioStrategyChanged
* TargetAllocationChanged

---

## FinancialPlanningService

Responsible for:

* Create Financial Plan
* Activate Financial Plan
* Archive Financial Plan
* Create Financial Goal
* Update Financial Goal
* Complete Financial Goal
* Update Planning Assumptions
* Assign Portfolio

Owns:

* FinancialPlan
* FinancialGoal
* PlanningAssumption
* PortfolioAssignment

Publishes:

* FinancialPlanCreated
* FinancialPlanActivated
* FinancialGoalCreated
* FinancialGoalCompleted
* PlanningAssumptionChanged

---

## IntelligenceService

Responsible for:

* Generate Insight
* Generate Recommendation
* Detect Risk
* Detect Opportunity
* Create Alert

Owns:

* Insight
* Recommendation
* RiskAssessment
* Opportunity

Consumes:

* PositionRecalculated
* PortfolioMetricsCalculated
* FinancialPlanProgressCalculated

Publishes:

* InsightGenerated
* RecommendationGenerated
* RiskDetected
* OpportunityDetected

---

## DashboardService

Responsible for:

* Create Dashboard
* Configure Dashboard
* Add Widget
* Remove Widget
* Generate Report
* Save View

Owns:

* Dashboard
* Widget
* Report
* SavedView

Publishes:

* DashboardCreated
* ReportGenerated

---

## DocumentService

Responsible for:

* Upload Document
* Import Document
* Generate Document
* Update Metadata
* Archive Document
* Restore Document

Owns:

* Document
* DocumentMetadata
* DocumentVersion

Publishes:

* DocumentUploaded
* DocumentGenerated
* DocumentArchived

---

## NotificationService

Responsible for:

* Create Notification
* Deliver Notification
* Mark Notification as Read
* Archive Notification

Owns:

* Notification
* NotificationDeliveryStatus

Consumes:

* business events from other services

Publishes:

* NotificationCreated
* NotificationDelivered
* NotificationRead

---

## AuditService

Responsible for:

* Record Audit Event
* Search Audit History
* Export Audit Records

Owns:

* AuditRecord
* ComplianceEvent
* AuditTrail

Consumes:

* sensitive business events from all services

Publishes:

* AuditRecordCreated

---

## TaxService

Responsible for:

* Configure Tax Profile
* Calculate Tax Position
* Generate Tax Report
* Recalculate Fiscal History

Owns:

* TaxProfile
* TaxLot
* FiscalEvent
* TaxReport

Publishes:

* TaxProfileConfigured
* TaxReportGenerated
* FiscalHistoryRecalculated

---

## AiAssistantService

Responsible for:

* Answer Question
* Explain Recommendation
* Summarize Dashboard
* Explain Portfolio
* Explain Financial Plan

Owns:

* AIConversation
* Explanation
* Summary

Consumes:

* authorized information from other services

Publishes:

* AIConversationStarted
* AIExplanationGenerated
* AISummaryGenerated

---

# 9. Forbidden Patterns

The following patterns are forbidden:

* Controller contains business logic.
* CommandHandler modifies aggregates directly without ApplicationService.
* ApplicationService performs financial calculations outside FinancialEngineService.
* ApplicationService directly updates another module's aggregate.
* ApplicationService accesses another module's database tables directly.
* QueryHandler modifies state.
* AI Assistant bypasses authorization or module boundaries.
* Dashboard calculates financial values.
* Portfolio stores owned performance values.

---

# 10. Implementation Contract

## Responsibilities

This document defines:

* official Application Services;
* ownership of use case orchestration;
* write operation flow;
* read operation flow;
* cross-service collaboration;
* forbidden implementation patterns.

## Required Implementation Pattern

Every write feature must generate:

* Command;
* CommandHandler;
* ApplicationService method;
* Validator;
* DTO or result object;
* Repository interaction if persistence is needed;
* Domain Events where applicable;
* Unit tests;
* Integration tests.

Every read feature must generate:

* Query;
* QueryHandler;
* DTO or read model;
* authorization validation;
* tests.

## Allowed Dependencies

Application Services may depend on:

* owned aggregates;
* owned repositories;
* domain services;
* public interfaces from other modules;
* event publisher;
* current user context;
* clock abstraction.

## Forbidden Dependencies

Application Services must not depend on:

* controllers;
* frontend code;
* infrastructure implementation details;
* another module's internal repository;
* another module's internal entities;
* direct database access.

---

# 11. AI Implementation Notes

AI coding agents must follow this document as an implementation contract.

When implementing a feature, AI must:

1. Identify the owning Application Service.
2. Create or update the appropriate Command or Query.
3. Implement the handler.
4. Delegate orchestration to the Application Service.
5. Keep business rules inside Aggregates or Domain Services.
6. Generate tests together with production code.
7. Preserve module boundaries.
8. Avoid inventing new services unless explicitly required.

AI must not create alternative patterns for similar features.

Consistency is more important than local optimization.

---

# 12. Acceptance Criteria

This document is complete when:

* every Application Service is identified;
* write and read flows are defined;
* ownership rules are explicit;
* service responsibilities are documented;
* forbidden patterns are listed;
* AI implementation rules are clear.

---

# 13. Change Log

| Version | Description                                |
| ------- | ------------------------------------------ |
| 0.1     | Initial Application Services architecture. |
