---
title: "Roadmap"
audience: [internal]
roles: [engineering, product]
onboarding:
  order: 7
  prerequisites: [technical/decisions]
  summary: What's deferred to Phase 2 and beyond, and why
  estimate: 5m
status: current
owner: tom@loomery.com
updated: 2026-08-17
---

> **Demo brain.** Simulated roadmap for a fictional client — see
> [[onboarding-status]].

# Roadmap

One-paragraph purpose: what's next after Phase 1, so a new team member doesn't propose
something already planned or already ruled out. See [[engagement]] for the current
phase and [[decisions]] for why some of this was deferred rather than
built now. See [[changelog]] for what's shipped of Phase 1 so far.

## Phase 2 — Compliance reporting

Audit-ready exports for regulators, building directly on the override-approval record
design Phase 1 already ships (see [[architecture]]). Not started; scoping
begins once Phase 1 is live at the Raccoon City pilot site. (source: [Google Drive](https://drive.google.com/file/d/1A9nB3vQeXyZpR7mK2dF8hLtC5wS4oJq6/view),
"Umbrella × Loomery — SOW v1.2")

## Watching, not committed

- **Group-wide template**: if the Raccoon City cutover goes cleanly, Group CIO Wendy
  Ashford has flagged interest in adapting Hive OS for Umbrella Pharmaceuticals' and
  Umbrella Consumer Health's own legacy plant-ops systems — see [[engagement]]
  §Group interest. Nothing scoped yet; this is a precondition, not a plan.
- **Remaining site cutovers**: Barcelona, Osaka, Cape Town, Vancouver, and Warsaw each
  follow Raccoon City once its pilot proves out, per the strangler-fig approach in
  [[decisions]]. Sequencing across the remaining five sites hasn't been
  discussed yet. (source: Granola note "Discovery: Facility Access Workflows",
  2026-07-02)
