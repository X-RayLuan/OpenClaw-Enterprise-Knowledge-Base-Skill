# OpenClaw Agent Sync

An OpenClaw-ready vault should include `openclaw/manifest.json`.

Minimal manifest:

```json
{
  "name": "enterprise-knowledge-base",
  "entrypoint": "Home.md",
  "hot_cache": "hot.md",
  "startup_order": [
    "openclaw/manifest.json",
    "hot.md",
    "Home.md"
  ],
  "safe_paths": [
    "Home.md",
    "hot.md",
    "00-Dashboard/",
    "actions/",
    "company/",
    "evidence/",
    "products/",
    "sales/",
    "service/"
  ],
  "governance": {
    "respect_status": true,
    "respect_visibility": true,
    "human_approval_required_for": [
      "price",
      "delivery_date",
      "warranty",
      "contract_terms",
      "customer_data_export",
      "public_publishing",
      "compliance_claims",
      "delete_knowledge"
    ]
  }
}
```

Agent startup behavior:

1. Read `openclaw/manifest.json`.
2. Read `hot.md` for current navigation context.
3. Read `Home.md` for durable knowledge map.
4. Follow object links and action pages as needed.
5. Refuse or escalate when governance rules require approval.

