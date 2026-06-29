# AI_ASSISTANT

Document ID: CAP-AI-001
Version: 1.0
Status: Accepted
Owner: Product & Architecture

## Depends On

* FINANCIAL_INTELLIGENCE
* FINANCIAL_ENGINE

---

# 1. Purpose

The AI Assistant helps users understand the Wealth Platform by providing explanations, summaries and contextual assistance.

The AI Assistant never replaces deterministic business logic.

---

# 2. Responsibilities

Responsible for:

* answering user questions;
* explaining financial concepts;
* summarizing information;
* assisting navigation;
* explaining recommendations.

Not responsible for:

* financial calculations;
* business decisions;
* modifying financial information.

---

# 3. Business Concepts

## AI Conversation

Contextual interaction between the user and the AI Assistant.

---

## Explanation

Natural language description of deterministic results.

---

## Summary

Condensed representation of business information.

---

# 4. Business Operations

* Answer Question
* Explain Recommendation
* Summarize Dashboard
* Explain Portfolio
* Explain Financial Plan

---

# 5. Business Rules

### BR-001

AI never generates financial truth.

### BR-002

Every explanation references deterministic information.

### BR-003

AI recommendations are advisory only.

### BR-004

Users remain responsible for financial decisions.

### BR-005

AI may orchestrate information retrieval across capabilities. AI never bypasses business capability boundaries.

---

# 6. Capability Interfaces

Consumes:

* Financial Intelligence
* Financial Engine
* Dashboard
* Documentation

Produces:

* Explanations
* Summaries
* Conversations

---

# 7. Dependencies

Consumes:

* Financial Intelligence
* Financial Engine
* Dashboard
* Notification

Provides:

* Conversational Interface

---

# 8. Security Considerations

* AI respects Workspace permissions.
* AI never exposes unauthorized information.
* Conversations follow audit policies where applicable.

---

# 9. AI Considerations

The AI Assistant is itself an AI capability.

Its behavior must remain:

* explainable;
* transparent;
* deterministic whenever possible;
* subordinate to business rules.

---

# 10. Acceptance Criteria

* AI responsibilities documented.
* Boundaries clearly defined.
* Deterministic principles preserved.

---

# 11. Open Questions

Future versions may support proactive assistance.

---

# 12. Change Log

| Version | Description           |
| ------- | --------------------- |
| 0.1     | Initial specification |
