# SVN → Git Migration (Release Trains + Standardized CI)

## What was improved?
- **Source control modernization:** moved from centralized SVN to Git with pull requests, required checks, and branch protections.
- **Branching governance:** implemented a **rolling 3-train release model** (Main + R1/R2/R3) to keep multiple releases in-flight without long-lived drift.
- **Delivery consistency:** standardized CI pipelines (build/test/tag/archive/deploy/notify) so teams inherited the same quality gates and release traceability.

## What was the impact?
- **Reduced late-cycle merge pain** by continuously forward-merging changes across active release trains.
- **Improved release confidence** through consistent PR validation and automated packaging + deploy steps.
- **Better traceability** from commit → build → artifact → deployment via deterministic tagging and artifact archival.

## Did it scale?
- Yes: the model supported **multiple repos and teams** by codifying rules (PR requirements, protections, merge responsibilities) and providing **template CI pipelines** that could be applied repo-by-repo.
- Release engineering tasks were centralized/automated (forward merges, release cut procedures), while teams kept autonomy on feature development.

## Was there measurable business value?
- Lower release risk (fewer “surprise” conflicts near ship date), faster recovery (clean rollback points), reduced manual release effort, and more predictable release cadence.
- Recommended metrics to prove value: PR lead time, build time, merge-conflict incidents per release, hotfix count, deployment frequency, and change failure rate.

## 60-second version
> “Led a migration from SVN to Git with a focus on keeping releases moving. Beyond converting repositories, I introduced governance: protected branches, PR approvals, and required CI checks. We used a rolling three-release-train strategy—Main for production, plus R1, R2, and R3 for sequential upcoming releases—where changes flowed forward to keep trains synchronized, and trains rotated after a release. I standardized the CI pipeline into reusable templates covering build, test, tagging, artifact archival, deploy, and notifications. The result was fewer late-cycle merge surprises, better traceability from commit to deploy, and a scalable model we could roll out across repos and teams.”

## Deep-dive prompts (if the interviewer asks)
- Why release trains vs GitFlow/trunk-only?
- How did you enforce protections and required checks?
- How did you handle hotfixes and backports?
- What did you measure before/after?
