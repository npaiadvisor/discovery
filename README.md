# Nonprofit AI Commons

Open patterns, starter repos, and a guided setup skill for **co-building practical AI assistants with nonprofits** — from a one-room workshop to a system the organization owns, runs, and maintains for itself.

Maintained by [npaiadvisor](https://github.com/npaiadvisor) (Brian Flett, in partnership with Management Advisory Services). Built in the open — contributions from fellow nonprofit-AI practitioners are welcome.

> **Status:** early. The repos are being populated from two production systems. Watch this space or open an issue to get involved.

## Why this exists

Most "AI for nonprofits" pilots die at handoff: the consultant leaves and the system rots because no one on staff can change it. This commons is built around the opposite goal — **self-sufficiency as the deliverable**. Every pattern here is designed so a non-technical nonprofit can operate, maintain, and evolve its assistant using a coding agent it talks to in plain English, with the safety rails living in the plumbing (preview-before-production), not in trusting any one AI.

## The two assistant shapes

Real nonprofit assistants fall into one of two shapes. The commons ships a starter for each.

| | **Shape A — Custom app** | **Shape B — Knowledge-base assistant** |
|---|---|---|
| Stack | Next.js + Vercel + Neon + OpenRouter | A hosted assistant (Claude Project / ChatGPT / Copilot / Gemini) + a knowledge base |
| UI | An admin dashboard | Chat *is* the UI — nothing to host |
| Best for | Monitor sources → AI brief → human-reviewed action | Q&A grounded in the org's own systems + guided, confirmation-gated actions |
| Rough cost | ~$40–100/mo | ~$8/seat, no hosting |
| Starter | [`app-starter`](https://github.com/npaiadvisor/app-starter) | [`kb-assistant-starter`](https://github.com/npaiadvisor/kb-assistant-starter) |

## Repos in the commons

- **`discovery`** (this repo) — the guided setup skill + the methodology library.
- **[`app-starter`](https://github.com/npaiadvisor/app-starter)** — Shape A: a custom AI web-app, de-domained from a production donor-outreach system.
- **[`kb-assistant-starter`](https://github.com/npaiadvisor/kb-assistant-starter)** — Shape B: an LLM-agnostic knowledge-base assistant.

## The `np-ai-discovery` skill

A [Claude Code](https://claude.com/claude-code) skill (in [`.claude/skills/np-ai-discovery/`](.claude/skills/np-ai-discovery/)) that walks a nonprofit from idea to scaffolded assistant:

1. **Scope** the first useful application (map the work → find the time-sink → name the objective).
2. **Interview the environment** — office suite (Microsoft 365 / Google / neither), CRM, the LLM you'll use, email sender.
3. **Pick the shape** (A or B) from the scoped problem.
4. **Scaffold** the right starter — write the config, select the connectors, and lay out the handoff runbook.

*Status: in development. See [`docs/`](docs/) for the methodology it operationalizes.*

## Methodology

The [`docs/`](docs/) folder holds the sanitized, reusable version of the method behind the starters — the adoption journey, the productionalization model, and the platform/subscription decision guide. (Population in progress.)

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Anyone may open issues and PRs. Everything here must pass [SANITIZATION.md](SANITIZATION.md) — no client data, no secrets.

## License

Code is [MIT](LICENSE). Documentation and case studies are [CC BY-SA 4.0](LICENSE-docs). Authors retain copyright; the license is a grant, not a transfer.
