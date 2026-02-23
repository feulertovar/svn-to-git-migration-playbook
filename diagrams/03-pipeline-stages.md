# CI pipeline stages (Build → Test → Tag/Build → Archive → Deploy → Notify)

```mermaid
flowchart TD
  A[Checkout] --> B[Build]
  B --> C[Test]
  C --> D{Is this a release-eligible branch?\n(main or active release train)}
  D -- No --> N[Stop after validation\n(PR checks reported)] --> Z[Notify\n(PR status)]
  D -- Yes --> E[Tag + Build\n(immutable version)]
  E --> F[Archive artifact\n(repo / artifact store)]
  F --> G[Security scans\n(SAST / dependency)]
  G --> H[Deploy to non-prod\n(dev/qa/stage)]
  H --> I{Promotion / approvals required?}
  I -- Yes --> J[Approval gate]
  J --> K[Deploy to prod]
  I -- No --> K[Deploy to prod]
  K --> L[Notify\n(Slack/email + summary)]
```

**Notes**
- PRs validate quickly (Build/Test) and report status checks.
- Release branches run full packaging, archiving, scans, and promotion.
