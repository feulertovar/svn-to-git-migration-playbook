# Migration Playbook — SVN → Git (Sanitized)

This playbook covers a safe, repeatable migration from SVN to Git, with an emphasis on:
- preserving history,
- minimizing downtime,
- and rolling out a scalable governance + CI model.

## Phase 0 — Goals & constraints
Define:
- target Git hosting (GitHub/GitLab/Bitbucket)
- compliance requirements (approvals, audits)
- target branching strategy (this repo uses a 3-train release model)
- CI/CD target (Jenkins, CircleCI, etc.)
- artifact store and deploy mechanism (generic: artifact repository + automation tool)

## Phase 1 — Discovery
Checklist:
- [ ] Inventory SVN repos (owner, size, activity, dependencies)
- [ ] Identify trunk/branches/tags layout
- [ ] Identify build tooling and CI coupling to SVN revision numbers
- [ ] Identify binary artifacts (consider Git LFS or artifact repository)
- [ ] Determine cutover sequence (by criticality)

Deliverable: `repo-audit.csv` (template in `/playbook/templates/`)

## Phase 2 — Target operating model
### Governance
- PRs required
- required checks (build/test/security scan)
- minimum approvals (e.g., 2 for critical code)
- branch protections on `main` and `release/*`

### Branching
- Adopt release-train strategy: see `branching-release-trains.md`

### CI/CD
Standard pipeline stages (example):
1) Build
2) Test
3) Tagging + Build (release semantics)
4) Archive artifact
5) Deploy (env promotion)
6) Notify (chat/email)

## Phase 3 — Conversion
Recommended approach: **phased migration with mirroring**
- Keep SVN read/write during initial conversion to validate Git output
- Optionally mirror SVN commits into Git until cutover

Conversion steps (per repo):
- [ ] Create author mapping (SVN user → name/email)
- [ ] Convert using `git svn` or a dedicated migration tool
- [ ] Verify:
  - commit count parity
  - tags/branches mapping
  - file integrity checks
- [ ] Push to Git remote
- [ ] Apply protections and required checks
- [ ] Enable CI and run validation builds

## Phase 4 — Cutover
- [ ] Announce freeze window (short)
- [ ] Make SVN read-only
- [ ] Final sync
- [ ] Switch CI checkout to Git
- [ ] Validate: build → test → artifact → deploy (smoke)
- [ ] Officially cut developers over to Git

## Phase 5 — Post-cutover hardening
- [ ] Remove deprecated SVN hooks/jobs
- [ ] Document new workflow (PR, branching, releases, hotfixes)
- [ ] Add automation:
  - stale branch cleanup
  - scheduled forward merges (release trains)
- [ ] Track metrics (see `/metrics/`)

## Rollback plan (must-have)
If Git cutover fails:
- revert CI to SVN checkout
- keep SVN read-only only if safe; otherwise restore write access
- document failures and reattempt migration per repo

