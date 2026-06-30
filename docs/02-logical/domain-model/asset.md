# ASSET

Document ID: LOG-DM-006
Version: 0.1
Status: Draft
Owner: Product & Architecture

## Depends On

* DOMAIN_ARCHITECTURE.md
* AGGREGATE_CATALOG.md
* domain-model/README.md
* ASSET_MANAGEMENT Capability

---

# 1. Purpose

The Asset aggregate represents a financial or non-financial instrument that may become part of a user's wealth.

An Asset is a universal business concept.

It exists independently of any Workspace, Container or Position.

---

# 2. Aggregate Ownership

**Owning Capability:** Asset Management

The Asset aggregate defines the canonical description of investable or ownable assets.

Ownership of an Asset must never be confused with ownership of wealth.

Wealth ownership is represented by Positions.

---

# 3. Primary Business Entity

## Asset

Represents one identifiable investment or property.

Examples:

* Apple Inc.
* Bitcoin
* Euro
* Vanguard FTSE All-World ETF
* Apartment in Barcelona
* Gold Bullion

Assets exist independently of investors.

---

# 4. Supporting Entities

## AssetClassification

Represents the business classification of an Asset.

Examples:

* Equity
* ETF
* Mutual Fund
* Bond
* Cryptocurrency
* Cash
* Real Estate
* Commodity
* Private Equity
* Other

---

## MarketReference

Represents external identifiers.

Examples:

* ISIN
* Ticker
* CUSIP
* FIGI

---

# 5. Value Objects

## AssetId

Global unique identifier.

---

## AssetName

Official business name.

---

## Currency

Primary valuation currency.

---

## AssetStatus

Possible values:

* Active
* Delisted
* Inactive

---

# 6. Relationships

Asset is referenced by:

* Position

Asset may appear in:

* Transactions

Asset never owns:

* Positions
* Containers
* Portfolios
* Financial Plans

---

# 7. Business Invariants

## AI-001

Every Asset has exactly one canonical identity.

---

## AI-002

Assets exist independently of ownership.

---

## AI-003

Multiple Positions may reference the same Asset.

---

## AI-004

Deleting an Asset never removes historical Positions.

---

## AI-005

Asset metadata may evolve without changing historical financial calculations.

---

# 8. Lifecycle

```text
Created
    │
    ▼
Active
    │
    ▼
Inactive
```

Rules:

* Historical Assets remain available.
* Delisted Assets preserve their history.
* Historical Positions remain valid.

---

# 9. Domain Events

Published:

* AssetCreated
* AssetUpdated
* AssetDelisted
* AssetReclassified

Consumed:

* ExternalAssetImported

---

# 10. Business Operations

* Register Asset
* Update Asset
* Reclassify Asset
* Delist Asset

---

# 11. Ownership Rules

Asset owns:

* Canonical identity
* Classification
* External references

Asset never owns:

* Wealth
* Positions
* Transactions
* Portfolios

---

# 12. Implementation Constraints

The Asset aggregate represents the global catalog of assets.

Portfolio ownership is always represented through Positions.

Financial calculations are never performed by the Asset aggregate.

---

# 13. Acceptance Criteria

The Asset aggregate is complete when:

* canonical identity is defined;
* ownership boundaries are explicit;
* relationships with Position are documented;
* invariants are complete.

---

# 14. Open Questions

None.

---

# 15. Change Log

| Version | Description                         |
| ------- | ----------------------------------- |
| 0.1     | Initial Asset aggregate definition. |
