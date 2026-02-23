# What to Measure (to prove business value)

Pick a small set of metrics you can credibly capture before/after the migration.

## Flow / delivery metrics
- PR lead time (open → merged)
- Build duration (median + p95)
- Deployment frequency
- Change failure rate (rollbacks / hotfixes / incidents)
- Mean time to recover (MTTR)

## SCM quality metrics
- Merge conflict incidents per release train
- Revert frequency
- Long-lived branches count (staleness)

## Operational metrics
- CI queue time / executor saturation
- Manual release engineering hours per release
- Release readiness checklist completion time

## How to present
Frame as:
- baseline → change introduced → measured result → cost/risk reduction
