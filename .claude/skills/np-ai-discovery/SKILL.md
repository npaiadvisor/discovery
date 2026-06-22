---
name: np-ai-discovery
description: Guide a nonprofit from idea to a scaffolded AI assistant. Scope the first useful application, interview the client's environment (office suite, CRM, LLM, email), pick the assistant shape (custom app vs knowledge-base assistant), and scaffold the matching starter repo with the right connectors and a handoff runbook. Use when starting a new nonprofit AI build, or when a motivated nonprofit wants to set one up themselves.
---

# np-ai-discovery

> **Stub — in development.** This skill is the meta-layer of the Nonprofit AI Commons. The behavior below is the design intent; implementation is tracked in the project spec.

## What it does

1. **Scope the first application.** Map the user's work, find the highest-leverage time-sink, name the strategic objective the assistant will serve. Output: a one-paragraph scoped problem.
2. **Interview the environment.** Office suite (Microsoft 365 / Google / neither) → connector set + which free coding agent to start with. CRM (CiviCRM / Blackbaud / Salesforce NPSP / none). App-runtime LLM (OpenRouter default). Email sender.
3. **Pick the shape.**
   - Needs scheduled monitoring + an admin UI + drafted artifacts → **Shape A** (`app-starter`).
   - Conversational Q&A grounded in the org's systems + gated tool actions, no app → **Shape B** (`kb-assistant-starter`).
4. **Scaffold.** Clone the chosen starter, write its `client-config` and `.env.example`, prune unused connector modules, and emit a Phase-0 identity checklist (the accounts to create under the agent's own email).

## Status

Skeleton only. See the commons README and `docs/` for the methodology this operationalizes.
