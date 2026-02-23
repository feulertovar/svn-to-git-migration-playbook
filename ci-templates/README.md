# CI/CD Templates (Sanitized)

These examples are intentionally generic.
They model an enterprise pipeline that includes build/test/tag/archive/deploy/notify and can be adapted to:
- Jenkins Multibranch
- GitHub Actions
- CircleCI
- GitLab CI

Key design goals:
- deterministic builds
- traceable releases (tag → artifact)
- quality gates (tests + scanning)
- environment promotion

See:
- `jenkins/Jenkinsfile.multibranch.example`
- `jenkins/shared-library/` (pseudo-implementation)
