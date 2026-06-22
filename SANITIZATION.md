# Sanitization rule

Everything in this commons is **public**. Nothing client-specific or secret may ever be committed — not in code, docs, examples, fixtures, screenshots, or commit messages.

## Never commit

- **Client-identifying data** — names of specific client organizations or their staff, real contact records, real CRM/email content, real prospect or donor data.
- **Credentials** — API keys, tokens, passwords, OAuth client secrets, connection strings, `.env` files with real values.
- **Organization-internal infrastructure** — production database schemas, internal hostnames, account IDs, private workflow internals.
- **Unconsented third-party content** — material whose author has not agreed to redistribution under this repo's licenses.

## Instead

- Use **generic, invented examples** ("a community arts nonprofit", "Example Org").
- Use **placeholders** in config: `your-api-key`, `YOUR_ORG.org`, `postgresql://USER:PASS@HOST/DB`.
- Keep real secrets only in a local, git-ignored `.env.local`.
- When distilling from a real system, **strip the domain specifics** into the example/config layer and describe the *pattern*, not the client.

## Before every commit

- Skim the diff for the categories above.
- If anything client-specific or secret is present, remove it before committing.
