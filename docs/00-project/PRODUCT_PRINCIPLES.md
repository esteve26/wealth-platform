# PRODUCT_PRINCIPLES

Document ID: PROD-PRINC-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture
Depends On:
- PROJECT_CONSTITUTION.md
- PROJECT_PHILOSOPHY.md

---

# Purpose

This document defines the product principles that guide every product decision.

Unlike the Constitution, these principles may evolve over time, but every change must preserve the product identity.

---

# Business View

## PP1 — Automation over Manual Work
Whenever reliable automation is technically feasible, it is preferred over manual processes.

## PP2 — Trust before Intelligence
Users must trust the data before trusting any recommendation.

## PP3 — Explain before Recommend
Every recommendation must explain why it exists.

## PP4 — Portfolio First
Recommendations optimize portfolios, not individual assets.

## PP5 — One Source of Truth
Every financial number must originate from a deterministic calculation.

## PP6 — Progressive Disclosure
The platform must be simple for beginners while allowing advanced analysis.

## PP7 — Configuration over Complexity
Offer guided configuration instead of unlimited customization.

## PP8 — Transparency by Default
Users should always understand where data comes from and when it was synchronized.

## PP9 — Security is Part of the Experience
Security must increase confidence without making the platform difficult to use.

## PP10 — AI Augments, Never Replaces
AI helps users understand information. It never replaces the user's judgement.

---

# Engineering View

These principles have direct architectural implications.

| Principle | Engineering consequence |
|-----------|-------------------------|
| Automation | Every capability must evaluate connector support before manual workflows. |
| Trust | Every displayed value must be traceable to source data. |
| Explainability | Recommendation Engine must expose evidence used to produce every recommendation. |
| Portfolio First | Financial Engine evaluates portfolio metrics before asset-level optimisation. |
| One Source of Truth | All financial calculations belong to the Financial Engine. |
| Progressive Disclosure | UI complexity must increase gradually according to user actions. |
| Configuration | Prefer configurable templates over fully custom implementations. |
| Transparency | Synchronization metadata is part of the domain model. |
| Security | Sensitive actions require strong authentication. |
| AI | AI consumes verified outputs; it never generates financial calculations. |

---

# Decision Checklist

Before accepting a new feature, verify:

- Does it increase user trust?
- Can it be explained?
- Can it be automated?
- Is it portfolio-centric?
- Does it preserve deterministic calculations?
- Does it align with the Constitution?

If any answer is "No", the feature requires explicit review.

---

# Related Future Documents

- PRODUCT_VISION.md
- NORTH_STAR.md
- DOMAIN_MODEL.md
- BUSINESS_CAPABILITIES.md
