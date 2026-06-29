# TRANSACTION_MANAGEMENT

**Document ID:** CAP-TXN-001  
**Version:** 1.0  
**Status:** Accepted  
**Owner:** Product & Architecture

---

## Depends On

- PROJECT_CONSTITUTION.md
- PRODUCT_PRINCIPLES.md
- PRODUCT_VISION.md
- UBIQUITOUS_LANGUAGE.md
- BUSINESS_CAPABILITIES.md
- WEALTH_MODEL.md
- PORTFOLIO_MANAGEMENT.md
- ASSET_MANAGEMENT.md

## Required By

- DOMAIN_MODEL.md
- DATA_MODEL.md
- FINANCIAL_ENGINE.md
- PROVIDER_INTEGRATION.md
- TAX_MANAGEMENT.md
- DASHBOARD_SYSTEM.md
- AI_ARCHITECTURE.md

---

# 1. Purpose

Transaction Management is the business capability responsible for recording, preserving and interpreting every financial event that changes the wealth of a Workspace.

Transactions are the historical source of truth for how Positions are created, modified, transferred or reduced.

A Transaction explains **why** a Position changed.

A Position represents **the current state** derived from one or more Transactions.

---

# 2. Business Problem

Users may own assets across multiple providers:

- banks;
- brokers;
- exchanges;
- wallets;
- crowdlending platforms;
- manual records;
- private investments.

Each provider may describe transactions differently.

Without a unified Transaction model:

- historical wealth cannot be reconstructed;
- cost basis cannot be calculated reliably;
- taxes cannot be estimated correctly;
- portfolio evolution becomes unreliable;
- imported data cannot be audited;
- AI explanations become untrustworthy.

The platform must provide a normalized and immutable transaction history.

---

# 3. Business Value

Transaction Management provides:

- historical integrity;
- auditability;
- reliable Position reconstruction;
- accurate cost basis calculation;
- tax traceability;
- provider reconciliation;
- error detection;
- explainable portfolio evolution.

---

# 4. Scope

## Included

- Transaction recording.
- Imported transactions.
- Manual transactions.
- Transaction normalization.
- Transaction immutability.
- Transaction correction.
- Fees and commissions.
- Transfers.
- Income events.
- Transaction source traceability.
- Transaction-to-Position impact.

## Excluded

- Direct financial advice.
- Automated trade execution.
- Tax filing.
- Provider-specific sync implementation.
- Database ledger schema.

---

# 5. Core Principles

## Transactions are immutable

Once created, a Transaction must not be edited or deleted.

Corrections must be represented through additional correcting Transactions.

## Transactions explain change

A Transaction explains why wealth changed.

## Transactions affect Positions

Transactions modify Positions.

They do not directly modify Portfolios.

## Imported transactions are provider evidence

Transactions imported from providers represent external evidence and must preserve their source metadata.

## Manual transactions are user-declared evidence

Manual transactions are allowed, but must remain distinguishable from imported transactions.

---

# 6. Transaction Types

The platform must support at least the following Transaction Types.

| Type        | Description                                          |
| ----------- | ---------------------------------------------------- |
| Buy         | Acquisition of an Asset.                             |
| Sell        | Disposal of an Asset.                                |
| Deposit     | Inflow of Cash or Asset into a Container.            |
| Withdrawal  | Outflow of Cash or Asset from a Container.           |
| Transfer    | Movement between Containers.                         |
| Dividend    | Income distribution from an Asset.                   |
| Interest    | Interest income.                                     |
| Salary      | Employment income deposited into a Container.        |
| Fee         | Commission, custody fee, trading fee or network fee. |
| Tax Payment | Tax-related outflow.                                 |
| Reward      | Staking, lending or promotional reward.              |
| Adjustment  | Correcting transaction used to fix errors.           |

Future Transaction Types may be added without changing the core model.

---

# 7. Fees and Commissions

Fees are first-class financial components.

A Transaction may include one or more Fees.

Fees may be paid in:

- cash;
- the acquired asset;
- the disposed asset;
- another asset.

Examples:

```text
Buy BTC
Amount: 1 BTC
Paid with: EUR
Fee: 10 EUR
```

```text
Buy ETH
Amount: 2 ETH
Fee: 0.01 ETH
```

Fees must be traceable because they affect:

- cost basis;
- realized profit/loss;
- provider comparison;
- tax estimation;
- portfolio performance.

---

# 8. Transaction Source

Every Transaction must have a Source.

Supported sources:

| Source            | Description                                                    |
| ----------------- | -------------------------------------------------------------- |
| Provider Import   | Imported from bank, broker, exchange or external platform.     |
| CSV Import        | Imported from user-provided file.                              |
| Manual Entry      | Entered manually by the user.                                  |
| System Adjustment | Created by the system to correct or reconcile inconsistencies. |
| Migration         | Created during data migration.                                 |

Imported Transactions should preserve raw provider references whenever possible.

---

# 9. Immutability and Corrections

Transactions must not be modified after creation.

If a Transaction is incorrect, the platform must create a new correcting Transaction.

Example:

```text
Original Transaction:
Buy BTC for 100 EUR

Correction:
Adjustment +20 EUR

Effective Cost:
120 EUR
```

This approach preserves:

- audit trail;
- historical reconstruction;
- source traceability;
- user trust.

Manual Transactions may be superseded, but not physically overwritten.

---

# 10. Transaction Lifecycle

```text
Discovered
  ↓
Normalized
  ↓
Validated
  ↓
Posted
  ↓
Corrected / Reversed
```

## Discovered

The transaction has been detected but not yet normalized.

## Normalized

The transaction has been mapped into the platform transaction model.

## Validated

The transaction has passed business validation.

## Posted

The transaction affects Positions.

## Corrected / Reversed

The transaction remains historically visible but has been corrected by a subsequent event.

---

# 11. Business Rules

## BR-001 — Transactions are immutable

A posted Transaction must not be edited or deleted.

## BR-002 — Corrections require new Transactions

Any correction must be represented by an Adjustment, Reversal or Correcting Transaction.

## BR-003 — Every Transaction belongs to one Workspace

Transactions are always scoped to exactly one Workspace.

## BR-004 — Every Transaction has a Source

A Transaction must identify how it entered the platform.

## BR-005 — Imported Transactions preserve provider metadata

External identifiers, timestamps and raw references must be preserved where available.

## BR-006 — Transactions affect Positions

Transactions create, increase, decrease or move Positions.

## BR-007 — Transactions do not directly modify Portfolios

Portfolios reflect the Positions assigned to them.

## BR-008 — Fees are explicit

Fees must be recorded separately from the main transaction amount.

## BR-009 — Multi-currency is supported

Transactions may involve more than one currency.

## BR-010 — Transfers must preserve continuity

A Transfer between Containers should not be treated as a taxable disposal unless explicitly required by tax rules.

## BR-011 — Manual Transactions are distinguishable

Manual Transactions must be distinguishable from imported Transactions.

## BR-012 — Duplicate detection is mandatory

The platform must detect potential duplicate Transactions during import or synchronization.

---

# 12. Position Impact

Transactions create or modify Positions.

Examples:

## Buy

Creates or increases a Position.

```text
Buy 1 BTC in Kraken
→ Increase BTC Position in Kraken Container
```

## Sell

Reduces a Position and may generate realized gain/loss.

```text
Sell 0.5 BTC from Kraken
→ Decrease BTC Position
→ Create cash inflow
```

## Transfer

Moves quantity between Containers.

```text
Transfer 1 BTC from Binance to Ledger
→ Decrease Binance Position
→ Increase Ledger Position
```

## Fee

Reduces cash or asset quantity.

```text
Network fee: 0.0002 BTC
→ Decrease BTC Position
```

---

# 13. Reconciliation

The platform must support reconciliation between:

- provider balances;
- imported transactions;
- calculated Positions;
- user-visible Holdings.

If calculated Positions do not match provider balances, the platform should raise an issue for review.

Reconciliation issues must not silently modify historical Transactions.

---

# 14. Actors

Primary actors:

- Individual Investor
- Wealth Manager
- Financial Advisor
- Provider Connector
- CSV Importer

Secondary actors:

- AI Assistant
- Platform Administrator
- Reconciliation Service

---

# 15. Permissions

| Action                    | Owner | Advisor | Viewer | System |
| ------------------------- | :---: | :-----: | :----: | :----: |
| View Transaction          |   ✅   |    ✅    |   ✅    |   ✅    |
| Create Manual Transaction |   ✅   |   ✅*    |   ❌    |   ❌    |
| Import Transaction        |   ✅   |   ✅*    |   ❌    |   ✅    |
| Correct Transaction       |   ✅   |   ✅*    |   ❌    |   ✅    |
| Delete Transaction        |   ❌   |    ❌    |   ❌    |   ❌    |
| View Raw Provider Data    |   ✅   |   ✅*    |   ❌    |   ✅    |

\* Subject to delegated permissions.

---

# 16. Domain Events

Potential domain events:

- TransactionDiscovered
- TransactionNormalized
- TransactionValidated
- TransactionPosted
- TransactionCorrected
- TransactionReversed
- FeeRecorded
- TransferMatched
- DuplicateTransactionDetected
- ReconciliationIssueDetected

---

# 17. AI Considerations

AI may:

- explain transactions;
- summarize transaction history;
- detect unusual transaction patterns;
- explain why a Position changed;
- help classify imported transactions;
- suggest possible duplicate matches.

AI must not:

- create posted Transactions autonomously;
- modify Transactions;
- delete Transactions;
- decide tax treatment without deterministic rules;
- override provider evidence.

---

# 18. Acceptance Criteria

The capability is considered complete when:

- Transactions can be imported.
- Transactions can be entered manually.
- Posted Transactions are immutable.
- Corrections are represented through new Transactions.
- Fees can be recorded explicitly.
- Multi-currency Transactions are supported.
- Transactions affect Positions.
- Duplicate detection exists.
- Provider source metadata is preserved.
- Historical reconstruction is possible.

---

# 19. Open Questions

| ID     | Question                                                                                |
| ------ | --------------------------------------------------------------------------------------- |
| OQ-001 | Should manual draft transactions be editable before posting?                            |
| OQ-002 | Should imported Transactions require user confirmation before posting?                  |
| OQ-003 | How should complex corporate actions be represented?                                    |
| OQ-004 | Should crypto swaps be modeled as sell+buy or as a dedicated transaction type?          |
| OQ-005 | Should transfers between wallets always require matching source and destination events? |

---

# 20. Future Evolution

Future versions may include:

- corporate actions;
- stock splits;
- crypto swaps;
- staking rewards;
- lending income;
- margin transactions;
- automated reconciliation;
- tax-lot selection;
- lot-level accounting;
- advanced transaction matching;
- event-sourced ledger implementation.

---

# 21. Change Log

| Version | Description                                             |
| ------- | ------------------------------------------------------- |
| 0.1     | Initial Transaction Management capability specification |
