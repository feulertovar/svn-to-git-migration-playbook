# SVN → Git Migration Playbook (Release-Train Branching + CI Standardization)

Public-safe, reusable playbook for migrating legacy Subversion (SVN) repositories to Git **without losing delivery cadence**.
This repo includes:
- A sanitized migration playbook
- A **rolling 3-train release branching model** (Main + R1/R2/R3)
- CI/CD template examples (Jenkins, adaptable to other CI systems)
- Checklists, risk controls, and suggested metrics

## 60-second interview one-pager
See: [`/one-pagers/interview-one-pager.md`](one-pagers/interview-one-pager.md)

## Contents
- Playbook: [`/playbook/`](playbook/)
- Branching strategy: [`/playbook/branching-release-trains.md`](playbook/branching-release-trains.md)
- CI templates: [`/ci-templates/`](ci-templates/)
- Metrics: [`/metrics/what-to-measure.md`](metrics/what-to-measure.md)

## Diagrams
See: [`/diagrams/`](diagrams/)

## Notes on sanitization
This repo intentionally omits:
- company names, internal URLs, hostnames, repo names
- proprietary application identifiers and environment names
- internal security implementation details

Everything here is written to be **enterprise-realistic** while remaining safe to share publicly.
