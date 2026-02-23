# Jenkins Shared Library (Pseudo) — Steps

This is a minimal, sanitized outline of shared steps you can implement as a Jenkins Shared Library:

- `vars/calcVersion.groovy`
- `vars/tagRelease.groovy`
- `vars/publishArtifact.groovy`
- `vars/runSecurityScan.groovy`
- `vars/deploy.groovy`
- `vars/notify.groovy`

Why shared library?
- Standardizes pipelines across repos
- Centralizes security gates
- Makes upgrades safer (versioned library)

Example calling pattern inside Jenkinsfile:

```groovy
@Library('ci-shared@v1') _
pipeline {
  stages {
    stage('Tag') { steps { tagRelease() } }
    stage('Publish') { steps { publishArtifact() } }
    stage('Scan') { steps { runSecurityScan() } }
  }
}
```
