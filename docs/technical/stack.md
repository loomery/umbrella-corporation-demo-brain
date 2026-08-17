---
title: "Stack"
audience: [internal]
roles: [engineering]
onboarding:
  order: 5
  prerequisites: [technical/context]
  summary: Languages, frameworks, infrastructure, and the src/ submodule map
  estimate: 10m
status: current
owner: tom@loomery.com
updated: 2026-08-17
---

> **Demo brain.** Simulated stack for a fictional client — see
> [[onboarding-status]].

# Stack

One-paragraph purpose: what Umbrella Corporation is built with, and which `src/` submodule
each part lives in — check this before opening any submodule. See [[architecture]]
for how these pieces fit together during the migration.

## Submodules

None yet. This is a demo brain with no real client repository to add as a
`src/<RepoName>` submodule — see `src/README.md`. In a real engagement at this delivery
stage, `src/hive-os` (the new platform) would be added once the client grants repo
access; `src/umbra-legacy` would follow if the strangler-fig work needs to read the
legacy schema directly.

## Languages & frameworks

- **Hive OS (new platform)** — TypeScript throughout. React frontend; NestJS backend
  service (`facility-access`, `sample-inventory` as separate modules within one
  service for Phase 1, per [[decisions]]); PostgreSQL for all new data.
- **UMBRA (legacy, being replaced)** — VB.NET WinForms client against an on-prem
  Oracle 11g database, no API layer; integration during the strangler-fig period is a
  nightly batch export Marcus Webb's team runs from Oracle into a staging bucket Hive
  OS reads from.
(source: Granola notes, "Discovery: Facility Access Workflows" 2026-07-02 and
"Sprint 1 Planning" 2026-08-06)

## Infrastructure

- **Hosting**: AWS (Umbrella's existing enterprise agreement), ECS Fargate for the
  NestJS service, RDS for PostgreSQL.
- **Auth**: Okta SSO, badge-system integration handled separately by Daniel Osei's
  team on Umbrella's side (out of scope for Hive OS itself, Hive OS only consumes the
  badge events).
- **CI/CD**: GitHub Actions, per Loomery's default pipeline template — not yet
  confirmed against Umbrella's own change-control process, which Priya Anand's team
  will need to sign off before Phase 1 goes live at the Raccoon City pilot site.
(source: Granola note "Sprint 1 Planning", 2026-08-06)
