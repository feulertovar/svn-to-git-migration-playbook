# Branching Strategy — Rolling 3-Train Release Model (Main + R1/R2/R3)

This model is designed for organizations that:
- need **multiple releases in flight** at the same time,
- want **fast integration** (trunk principles),
- and must avoid long-lived branch drift.

## Branches
- `main`: represents **production** (or the production-ready line).
- `release/R1`: next release (closest to shipping).
- `release/R2`: subsequent release.
- `release/R3`: future release.

Only **three release branches** are active at any given time.

## Merge flow (continuous forward merges)
Changes are regularly forward-merged to keep trains synchronized:

`release/R1 → main → release/R2 → release/R3`

### Why forward merges?
Forward merges prevent “merge debt” from accumulating and reduce the chance of a painful integration event late in a release.

## Release rotation (when R2 ships)
At ship time for R2:

1) Merge `release/R2 → main` (release cut / ship merge).
2) Rotate trains:
- Old `release/R2` becomes the new `release/R1`
- Old `release/R3` becomes the new `release/R2`
- Create a **new** `release/R3` from `main`

3) Resume forward merges:
`release/R1 → main → release/R2 → release/R3`

## Feature work
Recommended:
- short-lived `feature/*` branches off of `main` or the appropriate release train (depending on policy),
- PRs required to merge into the target branch.

## Hotfixes
Typical pattern:
- cut `hotfix/*` from `main`,
- validate via CI,
- merge back to `main` (ship),
- forward-merge to active release trains as needed.

## Ownership model
To keep merges consistent:
- Release/Build engineer owns **scheduled forward merges** and **release rotations**.
- Product teams own feature branches and cherry-picks (if required).

## Guardrails
- Protect `main` and `release/*` branches:
  - require PRs
  - require CI status checks
  - require approvals (e.g., 2 reviewers for critical repos)
- Prefer squash merges to keep history clean and make reverts simpler.

