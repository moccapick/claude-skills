# Domain Docs

How the engineering skills should consume this repo's domain documentation when exploring the codebase.

This is a **multi-context** repo: it is a skills library organised into independent domain folders (marketing, engineering, product, c-level advisory, project management, regulatory compliance, business growth, finance), each of which is self-contained and already carries its own `CLAUDE.md`.

## Before exploring, read these

- **`CONTEXT-MAP.md`** at the repo root if it exists — it points at one `CONTEXT.md` per context. Read each one relevant to the topic.
- Per-context **`CONTEXT.md`** inside the relevant domain folder (e.g. `engineering-team/CONTEXT.md`, `marketing-skill/CONTEXT.md`).
- Each domain's existing **`CLAUDE.md`** (e.g. `engineering-team/CLAUDE.md`) — the de-facto domain guide today; read it alongside any `CONTEXT.md`.
- **`docs/adr/`** at the root for system-wide decisions, plus `<domain>/docs/adr/` for context-scoped decisions, when present.

If any of these files don't exist, **proceed silently**. Don't flag their absence; don't suggest creating them upfront. The producer skill (`/grill-with-docs`) creates `CONTEXT.md` / `CONTEXT-MAP.md` lazily when terms or decisions actually get resolved.

## File structure

Multi-context layout (this repo — presence of `CONTEXT-MAP.md` at the root once created):

```
/
├── CONTEXT-MAP.md                      ← index of per-domain contexts (lazily created)
├── CLAUDE.md                           ← repo-wide navigation map
├── docs/adr/                           ← system-wide decisions
├── docs/agents/                        ← this skill's config (issue tracker, triage, domain)
├── engineering-team/
│   ├── CLAUDE.md
│   ├── CONTEXT.md                      ← lazily created
│   └── docs/adr/                       ← context-specific decisions
├── marketing-skill/
│   ├── CLAUDE.md
│   └── CONTEXT.md
└── …one folder per domain
```

## Use the glossary's vocabulary

When your output names a domain concept (in an issue title, a refactor proposal, a hypothesis, a test name), use the term as defined in the relevant context's `CONTEXT.md` (or that domain's `CLAUDE.md`). Don't drift to synonyms the glossary explicitly avoids.

If the concept you need isn't in the glossary yet, that's a signal — either you're inventing language the project doesn't use (reconsider) or there's a real gap (note it for `/grill-with-docs`).

## Flag ADR conflicts

If your output contradicts an existing ADR, surface it explicitly rather than silently overriding:

> _Contradicts ADR-0007 (event-sourced orders) — but worth reopening because…_
