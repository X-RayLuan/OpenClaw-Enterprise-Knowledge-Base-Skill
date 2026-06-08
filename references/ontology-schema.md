# Ontology Schema

## Object Page

```yaml
---
type: product
object_id: product-example
status: needs_review
visibility: internal
owner: sales
source:
  - internal
last_reviewed: 2026-06-08
---
```

## Relationship Style

Use explicit relationship sections.

```markdown
## Relationships

- has_certification:: [[CE]]
- suitable_for:: [[Outdoor-Handling]]
- quoted_by:: [[Quote-Template-Forklift]]
```

Relationship names should be stable lowercase snake_case verbs or verb phrases.

## Action Page

```yaml
---
type: action
action_id: create-quote-draft
status: verified
visibility: internal
owner: sales
allowed_roles:
  - sales_agent
requires_approval: true
risk_level: high
reads_from:
  - products
  - sales
writes_to:
  - quotes
last_reviewed: 2026-06-08
---
```

Action pages must define allowed inputs, output format, approval gates, and explicit prohibitions.

