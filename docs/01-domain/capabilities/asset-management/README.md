# ASSET_MANAGEMENT

**Document ID:** CAP-ASSET-001
**Version:** 1.0
**Status:** Accepted
**Owner:** Product & Architecture

---

# 1. Purpose

Asset Management is the business capability responsible for maintaining the canonical catalogue of financial and non-financial assets recognised by the Wealth Platform.

An Asset represents a unique economic entity that can be owned through one or more Positions.

Asset Management ensures that every Position references a single, normalized Asset regardless of the originating provider.

This capability acts as the **Master Data Management (MDM)** component for all assets in the platform.

---

# 2. Business Problem

Financial providers describe the same asset using different identifiers and formats.

Examples:

| Provider        | Identifier |
| --------------- | ---------- |
| Binance         | BTC        |
| Kraken          | XBT        |
| CoinGecko       | bitcoin    |
| Internal Import | Bitcoin    |

Without normalization:

* Portfolio composition becomes inconsistent.
* Holdings cannot be aggregated correctly.
* Financial calculations become unreliable.
* AI produces inaccurate recommendations.

---

# 3. Business Objectives

Asset Management must:

* Maintain one canonical definition per Asset.
* Automatically discover unknown Assets.
* Normalize identifiers from different providers.
* Prevent duplicate Assets.
* Preserve historical consistency.
* Support future expansion without redesign.

---

# 4. Scope

## Included

* Asset discovery
* Asset normalization
* Asset classification
* Asset identifiers
* Asset metadata
* Asset lifecycle
* Duplicate detection

## Excluded

* Price calculation
* Portfolio valuation
* Transaction processing
* Provider synchronization logic

---

# 5. Core Principles

## Assets are canonical

Every real-world asset has one canonical representation inside the platform.

---

## Assets are global

Assets are not owned by users.

Users own Positions.

---

## Assets are discovered

Creating Assets manually must be the exception.

The platform should discover Assets automatically whenever sufficient information is available.

---

## Human validation is exceptional

Human intervention should only be required when automatic discovery cannot safely identify an Asset.

---

# 6. Asset Discovery

The platform should automatically attempt to discover unknown Assets whenever they appear.

Typical sources include:

* imported transactions
* provider synchronization
* manual imports
* API integrations

Discovery is a business capability.

The implementation mechanism is defined elsewhere.

---

# 7. Asset Normalization

Different providers may describe the same Asset differently.

Example:

| Provider  | Value   |
| --------- | ------- |
| Binance   | BTC     |
| Kraken    | XBT     |
| CoinGecko | bitcoin |

All references must resolve to the same canonical Asset.

Normalization guarantees that:

* Holdings aggregate correctly.
* Positions remain consistent.
* Reports remain reliable.

---

# 8. Asset Classification

Each Asset belongs to one primary Asset Class.

Examples:

* Cash
* Equity
* ETF
* Mutual Fund
* Bond
* Cryptocurrency
* Stablecoin
* Commodity
* Precious Metal
* Real Estate
* Private Equity
* Crowdlending
* Art
* Vehicle
* Collectible
* Other

Future classifications may be added without changing the model.

---

# 9. Asset Lifecycle

```text
Discovered
      ↓
Pending Validation
      ↓
Active
      ↓
Inactive
```

Inactive Assets remain available for historical calculations.

Assets are never physically deleted.

---

# 10. Responsibilities

Asset Management is responsible for:

* Discovering Assets.
* Normalizing Assets.
* Managing metadata.
* Maintaining identifiers.
* Detecting duplicates.
* Governing Asset quality.
* Providing Asset information to other capabilities.

It is **not** responsible for:

* ownership
* Positions
* Holdings
* Transactions
* Portfolio calculations

---

# 11. Business Rules

**BR-001**

Every Position references exactly one canonical Asset.

**BR-002**

Canonical Assets are unique.

**BR-003**

Multiple external identifiers may reference the same Asset.

**BR-004**

Every Asset must belong to one Asset Class.

**BR-005**

Automatic discovery should be attempted before requesting manual validation.

**BR-006**

Manual validation should only occur when automatic normalization is insufficient.

**BR-007**

Assets are never permanently deleted.

---

# 12. Actors

Primary:

* Asset Discovery Service
* Platform Administrator

Secondary:

* Individual Investor
* Wealth Manager
* Financial Advisor
* AI Assistant

The Platform Administrator validates exceptional cases rather than maintaining the catalogue manually.

---

# 13. Domain Events

* AssetDiscovered
* AssetValidated
* AssetActivated
* AssetDeactivated
* AssetMerged
* AssetClassificationUpdated

---

# 14. Dependencies

Asset Management collaborates with:

* Provider Integration
* Transaction Management
* Portfolio Management
* Financial Engine
* AI Services

---

# 15. AI Considerations

AI may:

* explain Assets;
* detect duplicate candidates;
* suggest classifications;
* identify inconsistent metadata.

AI must not:

* create canonical Assets autonomously;
* merge Assets automatically;
* change classifications without validation.

---

# 16. Acceptance Criteria

The capability is considered complete when:

* Unknown Assets are automatically discovered.
* Duplicate Assets are prevented.
* Multiple provider identifiers map to one canonical Asset.
* Asset Classes are standardized.
* Historical Assets remain available.
* Human intervention is limited to exceptional cases.

---

# 17. Open Questions

| ID     | Question                                                          |
| ------ | ----------------------------------------------------------------- |
| OQ-001 | Should users create custom Assets for private investments?        |
| OQ-002 | How should delisted securities be represented?                    |
| OQ-003 | What minimum information is required before automatic activation? |

---

# 18. Future Evolution

Possible future enhancements:

* ESG classification
* Risk scoring
* Liquidity score
* Sector taxonomy
* Carbon footprint
* AI-generated descriptions
* Automatic provider confidence scoring

---

# 19. Change Log

| Version | Description                                                                                                                  |
| ------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 0.2     | Introduced automatic Asset Discovery, Normalization and MDM approach. Removed manual Asset creation as the default workflow. |
