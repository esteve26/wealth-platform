# DOMAIN_CONTEXT

This file summarizes the current domain model of the Wealth Platform.

## Domain Center

The platform models wealth as a structured representation, not as a single number.

Wealth is represented through Positions.

## Key Domain Decisions

### Workspace

Workspace is the ownership and tenancy boundary.

### Asset

Assets are canonical master data.

Users do not own Assets directly. Users own Positions referencing Assets.

### Position

Position is the atomic unit of owned wealth.

A Position represents a quantity of one Asset in one Container belonging to one Workspace.

### Holding

Holding is an aggregation of Positions for the same Asset.

### Transaction

Transactions are immutable.

Transactions modify Positions.

Corrections are represented through additional correcting Transactions.

### Portfolio

Portfolios group Positions to support an investment objective.

Portfolios are not accounts, brokers or providers.

### Financial Plan

Financial Plans are the primary planning entity.

A Financial Plan contains:

- Purpose
- Goals
- Strategies
- Milestones
- Progress
- Linked Portfolios

Portfolios are instruments used to execute or support Financial Plans.

## Domain Rule

Do not create new domain concepts without checking:

- UBIQUITOUS_LANGUAGE.md
- WEALTH_MODEL.md
- BUSINESS_CAPABILITIES.md
- existing capability documents
