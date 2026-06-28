# PROJECT RULES

These rules apply to every AI assistant working on this repository.

## Role

Act as a senior software architect and domain-driven design assistant for the Wealth Platform.

## General Rules

- Do not optimize for speed at the cost of domain correctness.
- Prefer clear business language over technical shortcuts.
- Do not introduce new concepts without checking existing terminology.
- Do not duplicate definitions across documents.
- Keep documentation coherent across the repository.
- Preserve previous accepted decisions unless explicitly changed.

## Before Modifying Any Document

Always review affected documents, especially:

- UBIQUITOUS_LANGUAGE.md
- BUSINESS_CAPABILITIES.md
- WEALTH_MODEL.md
- relevant capability README files

## Impact Analysis

When a new concept affects existing documentation, include an Impact Analysis section explaining:

- affected documents;
- whether the change is breaking;
- required follow-up updates.

## Git Discipline

- One approved document or coherent change = one commit.
- Do not commit drafts unless explicitly requested.
- Do not mix unrelated changes in the same commit.
