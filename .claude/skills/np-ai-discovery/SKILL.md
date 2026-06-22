---
name: np-ai-discovery
description: Guide a nonprofit from a scoped idea to a scaffolded, deployable AI assistant. Scope the first useful application, interview the client's environment (office suite, CRM, LLM, email, coding agent), pick the assistant shape (custom app vs knowledge-base assistant), and scaffold the matching starter repo with the right connectors and a handoff runbook. Use when starting a new nonprofit AI build, or when a motivated nonprofit wants to set one up themselves.
---

# np-ai-discovery

Guide a nonprofit from a scoped idea to a **scaffolded, deployable AI assistant**. This skill runs the interview, picks the assistant shape, selects the connectors, and scaffolds the matching starter from the [Nonprofit AI Commons](https://github.com/npaiadvisor).

> **When to use.** At the **Build** stage — after a workshop or discovery conversation has surfaced a real problem worth solving. If the problem isn't scoped yet, Step 1 does light scoping; for deep discovery, run a workshop first. One nonprofit, one application at a time — restraint beats scope.

## What you produce

1. A one-paragraph **scoped problem** + the strategic objective it serves.
2. A filled **environment profile** (suite / CRM / app LLM / email / coding agent).
3. A **scaffolded starter** — a Shape A app fork or a Shape B assistant package — with config, `.env.example`, and connectors selected.
4. A **Phase-0 identity checklist** — the accounts to create under the agent's own email.

---

## Step 1 — Scope the first application

Ask one topic at a time; this is a conversation, not a form.

- **The time-sink.** "What recurring task eats the most time, or quietly doesn't get done because no one has time?"
- **The objective.** "What strategic goal would doing that better advance — fundraising, member retention, volunteer capacity, program reach?"
- **Success.** "Three months in, what would tell you this is working?"
- **The human in the loop.** "Who reviews the AI's output before anything goes out?" (There must be one — nothing sends automatically.)

**Output:** a one-paragraph scoped problem statement + the named objective. If the answer is "lots of things," pick the single highest-leverage one and say so.

---

## Step 2 — Interview the environment

Record each answer; they drive the shape and the connectors. (This operationalizes the platform & subscription guide in [`docs/`](../../docs/platform-and-subscription-guide.md).)

| Ask | Options | Drives |
|---|---|---|
| Office suite? | Microsoft 365 / Google Workspace / neither | Document + email connectors; which **free** coding agent to start with |
| CRM? | CiviCRM / Blackbaud / Salesforce NPSP / spreadsheet / none | CRM connector module |
| App-runtime LLM? | OpenRouter (default) / other | `OPENROUTER_AGENT_MODEL`; cost cap |
| Email sender? | Their Workspace/M365 / Resend / none | `FROM_ADDRESS` + transport |
| Existing AI subscription? | ChatGPT / Claude / Copilot / Gemini / none | The maintenance + (Shape B) assistant container — match what they already pay for |
| Budget posture? | $0 first / can spend ~$20-100/mo | Start-free coding agent vs. paid; hosting tier |

**Coding-agent default (start free):** Google shop → **Jules**; Microsoft shop → **GitHub Copilot** free tier; either → Jules is the universal $0 path. Migrate to a flat-rate paid agent (Codex / Claude Code, ~$20/mo) only on a real trigger (volume, repeated failures, a correctness scare, mobile need).

---

## Step 3 — Choose the shape

| Signal | → Shape |
|---|---|
| Needs **scheduled monitoring**, a **pipeline**, an **admin dashboard**, or **drafted artifacts** reviewed over time | **A — [`app-starter`](https://github.com/npaiadvisor/app-starter)** |
| Conversational **Q&A grounded in their own systems** + **guided, confirmation-gated actions**, no pipeline or app | **B — [`kb-assistant-starter`](https://github.com/npaiadvisor/kb-assistant-starter)** |
| Tight budget, no one to host/maintain a web app | Lean **B** (~$8/seat, nothing to host) |
| Real recurring workflow with state, history, and a UI staff log into | Lean **A** |

State the choice and the one-line reason. When genuinely split, prefer **B** — it's cheaper and easier for a small org to sustain.

---

## Step 4 — Scaffold

### Shape A — custom app (`app-starter`)

1. **Create the client repo** from the starter (under the agent's GitHub account/org, transferred to the client at handoff):
   `gh repo create <client-org>/<repo> --private --clone` then copy in the starter, **or** fork [`npaiadvisor/app-starter`](https://github.com/npaiadvisor/app-starter).
2. **Fill config** from the interview — `config/app.ts` env values + a local `.env.local` from `.env.example`: `APP_NAME`, `OPENROUTER_AGENT_MODEL`, `FROM_ADDRESS`, `ADMIN_ALLOWED_EMAILS` (developer + agent account).
3. **Prune connectors** to their environment — see [`config/README.md`](https://github.com/npaiadvisor/app-starter/blob/main/config/README.md). Google shop: keep `lib/dossiers/google-docs.ts` + Gmail, drop OneDrive/Graph. M365 shop: the reverse. Drop unused capture sources (e.g. Apify/LinkedIn).
4. **Customize the domain** — the worked example is donor outreach. Replace the domain tables in `lib/db/schema.ts`, the agent prompts in `prompts/`, the Zod contract in `lib/llm/schema.ts`, the email copy in `lib/email/`, and the schedule in `vercel.json`. Leave the core alone.
5. **Deploy** — Vercel + Neon; set the same env vars in the Vercel project. Confirm `pnpm build` is green and the health-check responds.

### Shape B — knowledge-base assistant (`kb-assistant-starter`)

1. Start from [`kb-assistant-starter`](https://github.com/npaiadvisor/kb-assistant-starter).
2. **Pick the container** matching their LLM: Claude Project / ChatGPT Custom GPT / Microsoft Copilot agent / Gemini Gem (use the per-vendor install notes).
3. Load the **system prompt + curriculum**; set up the **KB scope** (audience-scoped vector store) and ingestion of their source docs.
4. **Wire connectors** — CRM (read + confirmation-gated write), document store, database — via that vendor's connector mechanism.

---

## Step 5 — Handoff rails (set on the client's fork)

- **`AGENTS.md` + `CLAUDE.md`** present and current — the runbook the client's coding agent reads.
- **Branch protection: PR-only to `main`** on the client repo — every change gets a Vercel preview before production (Shape A). This is the safety model; it lives in the plumbing, not in trusting the LLM.
- **Maintenance Assistant** in the client's LLM, loaded with the runbook, so they change the system by talking to it.
- **Phase-0 identity:** create a dedicated agent Gmail (`<project>.ai@gmail.com`), then sign up for GitHub / Vercel / Neon / OpenRouter under it — so handoff is a single credential transfer.

---

## Sanitization (always)

The Commons repos are public. When scaffolding, never commit client data or secrets — see [`SANITIZATION.md`](../../SANITIZATION.md). The client's own repo may be private, but treat the starters and any contributed pattern as world-readable.
