---
name: openclaw-enterprise-knowledge-base
description: Use when creating, auditing, repairing, validating, or syncing an enterprise Markdown or Obsidian knowledge base for OpenClaw agents. Applies to ontology-style wiki pages, governed business objects, hot.md startup cache, agent-safe visibility rules, OpenClaw manifests, RAG handoff, sales/support action governance, and knowledge-base QA workflows.
version: "0.1.0"
tags:
  - openclaw
  - enterprise
  - knowledge-base
  - wiki
  - ontology
  - rag
mutating: true
---

# OpenClaw Enterprise Knowledge Base

Use this skill to turn enterprise wiki material into an agent-ready semantic layer for OpenClaw. The objective is not more notes. The objective is reliable agent behavior: verified facts, governed visibility, explicit relationships, approved actions, and a short startup cache.

## Core Model

Treat every important Markdown page as a business object.

```text
Markdown page = object
YAML frontmatter = object attributes
Wiki links / inline fields = relationships
Action pages = approved business verbs
status + visibility = governance and permissions
openclaw/manifest.json = runtime contract
hot.md = fresh-session startup cache
```

## When Starting

1. Decide whether the user is creating a new vault, auditing an existing vault, adding objects, or preparing OpenClaw sync.
2. For folder layout, read `references/vault-structure.md`.
3. For object fields and relationship style, read `references/ontology-schema.md`.
4. For object types, relationship predicates, action families, and governance vocabulary, read `references/ontology-vocabulary.md`.
5. For the root hot cache pattern, read `references/hot-cache.md`.
6. For OpenClaw runtime handoff, read `references/agent-sync.md`.

Ask only when the missing choice changes the artifact materially. Otherwise choose conservative enterprise defaults.

## Required Object Frontmatter

Every object page must include:

```yaml
---
type:
object_id:
status: needs_review
visibility: internal
owner:
source:
last_reviewed:
---
```

Allowed `status` values:

- `verified`: may be used externally if visibility allows it.
- `needs_review`: internal use only until a human verifies it.
- `conflicting`: known conflict exists; do not cite externally.
- `deprecated`: keep for history; do not use in active answers.

Allowed `visibility` values:

- `public`: customer-facing.
- `dealer`: partner-facing.
- `internal`: staff-facing.
- `management`: management-only.

## Hot Cache Rule

Create a root `hot.md` for the current working context. OpenClaw should read it before `Home.md`.

Use `hot.md` for:

- Current topic or active workstream.
- Key recent conclusions.
- Related pages to read next.
- One concrete next step.

Do not use `hot.md` for:

- Long-term policy.
- Full knowledge dumps.
- Customer-facing facts without source pages.
- Secrets, credentials, private customer data, or sensitive pricing.

## Action Governance

Actions are ontology verbs. Create action pages for agent behaviors such as quote drafting, product recommendation, service intake, or escalation.

Any action involving price, delivery date, warranty, contract terms, customer data export, public publishing, compliance claims, or deleting knowledge requires human approval.

Use the action families and approval gates in `references/ontology-vocabulary.md` when designing a reusable enterprise vault.

## OpenClaw Startup Order

OpenClaw-facing vaults should include:

```text
openclaw/manifest.json
hot.md
Home.md
```

The manifest should expose safe paths, approved action names, startup order, and governance rules. It must not bypass `status` or `visibility`.

## Validation

Run the bundled validator from this repo:

```bash
node scripts/validate-vault.mjs --vault /path/to/vault
```

Before finalizing a vault, confirm:

- Required frontmatter fields exist.
- `object_id` values are unique.
- Action pages include `action_id`.
- Public pages are verified.
- Action pages say what the agent may and may not do.
- `hot.md` is short and contains no sensitive data.
- OpenClaw startup order is explicit.
