# DOMAIN RULES

These are mandatory domain rules for the Wealth Platform.

## Core Invariants

- Workspace is the ownership and tenancy boundary.
- Wealth belongs to a Workspace.
- Asset is canonical master data.
- Position is the atomic unit of owned wealth.
- Holding is an aggregation of Positions.
- Transaction is immutable.
- Transaction modifies Positions.
- Portfolio groups Positions.
- Financial Plan defines planning purpose, goals, strategies, milestones and progress.
- Portfolio is an instrument supporting a Financial Plan.
- Provider is never the owner of user wealth.
- Financial Engine calculates financial truth.
- AI explains and assists but does not create financial truth.

## Terminology

Use the terms defined in UBIQUITOUS_LANGUAGE.md.

Do not use synonyms casually.

Examples:

- Use Position, not balance, when referring to atomic owned wealth.
- Use Provider, not platform, when referring to external financial institutions.
- Use Container, not account, when referring generally to where Positions exist.
- Use Financial Plan for planning context.
- Use Portfolio for investment grouping.

## New Concepts

Before introducing a new concept, answer:

1. Is it a business concept or a technical implementation detail?
2. Which capability owns it?
3. Which existing concepts does it relate to?
4. Does it affect existing documents?
5. Does it require an ADR?
