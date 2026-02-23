# Hotfix flow (cut from main, then forward-merge)

```mermaid
flowchart LR
  main[main\n(production)]:::main
  r1[R1]:::train
  r2[R2]:::train
  r3[R3]:::train

  %% Hotfix branch cut from production
  hf[hotfix/*\ncut from main]:::hotfix -->|PR (2 approvers + checks)| main

  %% After hotfix lands in main, propagate forward to keep trains in sync
  main -->|merge forward| r2
  r2 -->|merge forward| r3

  %% Optional: if R1 is active and must include hotfix behavior
  main -->|merge forward (if applicable)| r1

  classDef main fill:#e6f4ff,stroke:#1b74e4,stroke-width:2px;
  classDef train fill:#f3f4f6,stroke:#6b7280,stroke-width:1px;
  classDef hotfix fill:#ffe4e6,stroke:#be123c,stroke-width:1px;
```

**Decision rule:** hotfixes are cut from production (`main`) to minimize risk, then forward-merged so upcoming trains inherit the fix.
