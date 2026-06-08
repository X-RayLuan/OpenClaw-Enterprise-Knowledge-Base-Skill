# OpenClaw Enterprise Knowledge Base Skill

Reusable skill for turning an enterprise Markdown or Obsidian vault into an agent-ready knowledge base for OpenClaw.

The goal is simple: make company knowledge usable by agents without turning it into an unsafe note dump. Each important page is treated as a governed business object with required metadata, explicit relationships, action permissions, and a short hot cache that tells a fresh agent where to start.

## What This Skill Provides

- A practical ontology pattern for enterprise wiki pages.
- Required frontmatter for status, visibility, owner, source, and review date.
- OpenClaw startup rules, including a root `hot.md` hot cache.
- Governance rules for customer-facing answers and high-risk actions.
- A lightweight validator for frontmatter, duplicate IDs, and hot cache length.

## Repository Layout

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── agent-sync.md
│   ├── hot-cache.md
│   ├── ontology-schema.md
│   ├── ontology-vocabulary.md
│   └── vault-structure.md
├── scripts/
│   └── validate-vault.mjs
└── tests/
    └── validate-vault.test.mjs
```

## Quick Start

Create or update an enterprise vault with this shape:

```text
Enterprise-Vault/
├── hot.md
├── Home.md
├── 00-Dashboard/
├── actions/
├── evidence/
├── openclaw/
│   ├── README.md
│   └── manifest.json
├── products/
├── sales/
└── service/
```

Every object page should include:

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

OpenClaw should read in this order:

```text
openclaw/manifest.json -> hot.md -> Home.md
```

`hot.md` is a short startup cache, not a source of truth. Keep it under 500 Chinese characters or roughly 900 English characters.

## Validate A Vault

```bash
node scripts/validate-vault.mjs --vault /path/to/Enterprise-Vault
```

The validator checks:

- Markdown files with YAML frontmatter.
- Missing required object fields.
- Duplicate `object_id` values.
- Missing `action_id` values on action pages.
- Public pages that are not verified.
- `hot.md` body length.

## Ontology Coverage

The skill includes a reusable enterprise ontology vocabulary:

- Object types such as `company`, `product`, `certification`, `sales_scenario`, `quote_template`, `service_rule`, `action`, and `evidence`.
- Relationship predicates such as `has_certification`, `suitable_for`, `quoted_by`, `derived_from`, `requires_approval_from`, and `supersedes`.
- Action families for sales, support, knowledge maintenance, and escalation.
- Governance rules for status, visibility, approval gates, and wrong-answer correction.

See `references/ontology-vocabulary.md` when designing or auditing a real vault.

## Publishing Notes

This repo is designed to be published as a skill package. Keep company-specific facts, customer data, prices, quotes, internal disputes, and private source files out of this repository. Put only reusable operating rules here.
