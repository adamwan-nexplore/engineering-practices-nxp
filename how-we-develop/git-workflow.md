# Git Workflow <!-- omit in toc -->

Table of Contents

- [Introduction](#introduction)
- [Development](#development)
- [Hotfix](#hotfix)
- [Infrastructure Change](#infrastructure-change)

## Introduction

- We are currently on [GitLab Flow](https://about.gitlab.com/topics/version-control/what-is-gitlab-flow).

- We promote and aim at transiting to a linear flow based on `dev-deployment`
- The change from `dev-deployment` to all `uat-deployment` MUST be done through `git merge`
- The change from `uat-deployment` to all `prod-deployment` MUST be done through `git merge`

*We might switch to `trunk-based development` IF there are more environments. Check [here](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development "Trunk-based development - Learn why this version control management practice is common practice among DevOps teams."), [here](https://trunkbaseddevelopment.com "Trunk Based Development: Introduction") and [here](https://cloud.google.com/architecture/devops/devops-tech-trunk-based-development "Prevent merge-conflict hassles with trunk-based development practices")*

## Development

```mermaid
---
title: Branch Transition on Submitting a Feature / Fix
---
flowchart TD
    feature(feature/XXX)
    develop(dev-deployment)
    uat(uat-deployment)
    prod(prod-*-deployment)
    start([Start])
    finish([finish])

    dev-env[DEV ENV]
    uat-env[UAT ENV]
    prod-env[PROD ENVs]

    style develop stroke:#f00
    style uat stroke:#A020F0
    style prod stroke:#00f

    style dev-env fill:#f00
    style uat-env fill:#A020F0
    style prod-env fill:#00f

    start --> feature
    develop -->|branch out| feature -->|rebase| develop -->|merge| uat -->|sign-off & merge| prod --> finish

    develop -..->|deploy| dev-env
    uat -..->|deploy| uat-env
    prod -..->|deploy| prod-env
```

## Hotfix

```mermaid
---
title: Branch Transition on Hotfix
---
flowchart TD
    hotfix(hotfix/XXX)
    develop(dev-deployment)
    uat(uat-deployment)
    prod(prod-*-deployment)
    start([Start])
    finish([finish])

    dev-env[DEV ENV]
    uat-env[UAT ENV]
    prod-env[PROD ENVs]

    style develop stroke:#f00
    style uat stroke:#A020F0
    style prod stroke:#00f

    style dev-env fill:#f00
    style uat-env fill:#A020F0
    style prod-env fill:#00f

    start --> hotfix
    develop -->|branch out| hotfix -->|cherry-pick| uat -->|merge| develop
    hotfix -->|rebase| develop

    uat -->|sign-off & merge| prod --> finish

    uat -..->|deploy| uat-env
    prod -..->|deploy| prod-env
    develop -..->|deploy| dev-env
```

## Infrastructure Change

```mermaid
---
title: Branch Transition on Changing the infrastructure
---
flowchart TD
    feature(feature/XXX)
    sandbox(sbx-deployment)
    develop(dev-deployment)
    uat(uat-deployment)
    prod(prod-*-deployment)
    start([Start])
    finish([finish])

    sbx-env[SANDBOX ENV]
    dev-env[DEV ENV]
    uat-env[UAT ENV]
    prod-env[PROD ENVs]

    style sandbox stroke:yellow
    style develop stroke:#f00
    style uat stroke:#A020F0
    style prod stroke:#00f

    style sbx-env fill:yellow
    style dev-env fill:#f00
    style uat-env fill:#A020F0
    style prod-env fill:#00f

    start --> feature
    feature -->|rebase| sandbox
    sandbox -->|branch out| feature
    sandbox -->|merge| develop -->|merge| uat -->|sign-off & merge| prod --> finish


    sandbox -..->|deploy| sbx-env
    develop -..->|deploy| dev-env
    uat -..->|deploy| uat-env
    prod -..->|deploy| prod-env
```
