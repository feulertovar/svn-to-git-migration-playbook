# CI pipeline stages (Build → Test → Tag/Build → Archive → Deploy → Notify)

```mermaid
flowchart LR

  A["Checkout source"] --> B["Build application"]
  B --> C["Run tests"]

  C --> D{"Release eligible"}

  D -->|Yes| E["Tag and build release artifact"]
  D -->|No| N["Notify build result"]

  E --> F["Archive artifact to repository"]
  F --> G["Security scan"]
  G --> H["Deploy to environment"]
  H --> I["Notify deployment result"]
```

**Notes**
- PRs validate quickly (Build/Test) and report status checks.
- Release branches run full packaging, archiving, scans, and promotion.
