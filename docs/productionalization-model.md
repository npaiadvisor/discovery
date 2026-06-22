# Productionalization Model

> **Stub.** Sanitized, client-neutral version in progress.

A repeatable method for taking an AI-augmented internal tool from prototype to a self-sufficient, client-owned production system. After handoff, the nonprofit can **operate** it without the consultant, **maintain** it (small changes, content updates) using its own LLM, **evolve** it by hiring any mainstream contractor, and **pay** for it directly.

The maintenance loop, enforced by the plumbing rather than by trusting the AI:

> Ask a coding agent in plain English → it opens a pull request → a preview deploys against a throwaway database branch → a human eyeballs the preview → merge to production.

The default stack is mainstream and contractor-friendly: Next.js on Vercel, Postgres on Neon, an LLM via OpenRouter, repo on GitHub. The same stack holds regardless of whether the org runs Microsoft 365 or Google Workspace.
