# Vault Structure

Recommended enterprise vault layout:

```text
Enterprise-Vault/
├── hot.md
├── Home.md
├── 00-Dashboard/
│   ├── Agent-Actions.md
│   └── Review-Queue.md
├── actions/
├── company/
├── evidence/
├── openclaw/
│   ├── README.md
│   └── manifest.json
├── products/
├── sales/
├── service/
└── source-materials/
```

Use folders by business object type. Keep raw intake files under `source-materials/` and distilled, cited evidence notes under `evidence/`.

`Home.md` is the durable navigation hub. `hot.md` is the short fresh-session cache. Dashboards are operational views, not source-of-truth pages.

