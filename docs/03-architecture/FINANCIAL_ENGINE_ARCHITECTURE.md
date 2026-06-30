# FINANCIAL_ENGINE_ARCHITECTURE

Document ID: ARCH-FE-001
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* APPLICATION_ARCHITECTURE.md
* BOUNDED_CONTEXTS.md
* APPLICATION_SERVICES.md
* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md

---

# 1. Purpose

This document defines the architecture of the Financial Engine.

The Financial Engine is the only component responsible for producing derived financial state from immutable business events.

It is implemented as a deterministic calculation pipeline composed of independent calculation stages.

---

# 2. Architectural Decisions

## FE-001 — Single Source of Financial Truth

Only the Financial Engine may calculate:

* Positions
* Holdings
* Valuations
* Portfolio Metrics
* Financial Plan Progress
* Risk Metrics
* Allocation Metrics

No other module may calculate or persist derived financial values.

---

## FE-002 — Immutable Inputs

The Financial Engine never modifies Transactions.

Transactions represent immutable business history.

The engine only consumes them.

---

## FE-003 — Deterministic Execution

Identical inputs must always produce identical outputs.

No hidden state is allowed.

No random behaviour is allowed.

No calculation depends on execution order outside the defined pipeline.

---

## FE-004 — Pipeline Architecture

Calculations are executed through ordered Calculation Stages.

Each stage has:

* one responsibility;
* deterministic behaviour;
* explicit input;
* explicit output.

---

## FE-005 — Recalculation is Idempotent

Executing the pipeline multiple times with identical inputs must always produce identical outputs.

---

# 3. Financial Engine Responsibilities

The Financial Engine is responsible for:

* rebuilding Positions;
* rebuilding Holdings;
* calculating valuations;
* calculating allocations;
* calculating portfolio metrics;
* calculating financial plan progress;
* publishing financial calculation events.

It is not responsible for:

* importing data;
* user interaction;
* dashboards;
* AI recommendations;
* reporting.

---

# 4. Inputs

The engine consumes:

* Transactions
* Assets
* Exchange Rates
* Portfolio Definitions
* Financial Plans
* Planning Assumptions

Inputs are always read-only.

---

# 5. Outputs

The engine produces:

* Positions
* Holdings
* Portfolio Metrics
* Allocation Metrics
* Performance Metrics
* Financial Plan Progress
* Domain Events

Outputs become the official derived financial state.

---

# 6. Calculation Pipeline

The Financial Engine executes the following pipeline:

```text
Transaction/Event
        │
        ▼
Normalization Stage
        │
        ▼
Validation Stage
        │
        ▼
Position State Update Stage
        │
        ▼
Holding State Update Stage
        │
        ▼
Portfolio State Update Stage
        │
        ▼
Planning State Update Stage
        │
        ▼
Metrics Calculation Stage
        │
        ▼
Publish Domain Events
```

Stages execute sequentially.

A stage may only consume outputs produced by previous stages.

---

# 7. Calculation Stages

## Stage 1 — Normalization

Responsibilities:

* normalize currencies;
* normalize quantities;
* normalize timestamps;
* normalize transaction types;
* normalize imported provider data.

Produces:

* Canonical Financial Events.

---

## Stage 2 — Validation

Responsibilities:

* validate references;
* validate transaction integrity;
* validate asset existence;
* validate planning references.

Produces:

* Validated Financial Events.

---

## Stage 3 — Position Calculation

Consumes:

* Validated Financial Events.

Produces:

* Position snapshots.
* Position metrics.
* Position valuations.

Responsibilities:

* open positions;
* close positions;
* update quantities;
* calculate average cost;
* calculate cost basis;
* calculate market value;
* calculate unrealized gain or loss;
* calculate realized gain or loss;
* calculate position-level return;
* update last recalculation timestamp.

---

## Stage 4 — Holding Calculation

Consumes:

* Positions.

Produces:

* Holdings.

Responsibilities:

* aggregate Positions;
* group equivalent Positions;
* calculate holding quantities.

---

## Stage 5 — Portfolio Calculation

Consumes:

* Holdings;
* Portfolio definitions.

Produces:

* Portfolio Metrics.

Responsibilities:

* total value;
* allocation;
* diversification;
* exposure;
* portfolio composition.

---

## Stage 6 — Planning Calculation

Consumes:

* Portfolio Metrics;
* Financial Plans;
* Planning Assumptions.

Produces:

* Goal Progress;
* Planning Metrics.

Responsibilities:

* goal completion;
* projection updates;
* progress calculation.

---

## Stage 7 — Metrics Calculation

Consumes:

* Positions;
* Holdings;
* Portfolio Metrics.

Produces:

* Performance metrics;
* Allocation metrics;
* Historical metrics;
* Risk metrics (future extension).

---

## Stage 8 — Domain Event Publication

Publishes:

* PositionRecalculated
* HoldingRecalculated
* PortfolioMetricsCalculated
* FinancialPlanProgressCalculated

No calculations occur in this stage.

---

# 8. Trigger Sources

Pipeline execution may be triggered by:

* TransactionRecorded
* TransactionCorrected
* ProviderSynchronizationCompleted
* ExchangeRateUpdated
* AssetUpdated
* PlanningAssumptionChanged

Triggers never perform calculations directly.

They request pipeline execution.

---

# 9. Recalculation Strategy

The engine supports:

* Full Workspace Recalculation
* Portfolio Recalculation
* Financial Plan Recalculation
* Incremental Recalculation (future optimization)

The business result must be identical regardless of recalculation strategy.

---

# 10. Error Handling

If a stage fails:

* later stages are not executed;
* partial results are discarded;
* no derived financial state is persisted;
* an appropriate Domain Event is published.

Financial consistency has priority over availability.

---

# 11. Performance Principles

The Financial Engine must:

* minimize repeated calculations;
* support incremental recalculation;
* support parallel execution of independent work where deterministic;
* preserve deterministic behaviour.

Performance optimizations must never change business results.

---

# 12. Forbidden Patterns

The following are forbidden:

* Portfolio calculating financial metrics.
* Dashboard calculating financial values.
* AI generating financial values.
* Planning calculating progress independently.
* Controllers invoking calculation logic.
* Repositories containing business calculations.
* Duplicate calculation algorithms.

---

# 13. Implementation Contract

## Responsibilities

The Financial Engine owns all derived financial state.

## Allowed Dependencies

The engine may read:

* Transactions;
* Assets;
* Exchange Rates;
* Portfolios;
* Financial Plans.

The engine may publish:

* Domain Events.

## Forbidden Dependencies

The engine must not depend on:

* Controllers;
* UI;
* Dashboards;
* AI Assistant;
* Notification logic.

---

# 14. AI Implementation Notes

AI coding agents must implement the Financial Engine as a deterministic pipeline.

Each Calculation Stage should be implemented as an independent component with:

* explicit input;
* explicit output;
* no hidden mutable state.

Stages must be individually testable.

Pipeline orchestration must be separated from calculation logic.

AI agents must never duplicate calculation algorithms outside the Financial Engine.

---

# 15. Acceptance Criteria

This document is complete when:

* calculation ownership is explicit;
* the pipeline is defined;
* stages are documented;
* inputs and outputs are identified;
* recalculation rules are documented;
* implementation constraints are explicit.

---

# 16. Change Log

| Version | Description                            |
| ------- | -------------------------------------- |
| 0.1     | Initial Financial Engine architecture. |
