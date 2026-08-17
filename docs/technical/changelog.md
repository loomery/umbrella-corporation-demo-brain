---
title: "Changelog"
audience: [internal]
roles: [engineering, product, delivery]
onboarding:
  order: 8
  prerequisites: [technical/decisions]
  summary: What's shipped so far in Phase 1, sprint by sprint
  estimate: 5m
status: current
owner: tom@loomery.com
updated: 2026-08-17
---

> **Demo brain.** Simulated changelog for a fictional client — see
> [[onboarding-status]].

# Changelog

One-paragraph purpose: what Hive OS has actually shipped, sprint by sprint, since
Phase 1 delivery started — this is our own build log, not a vendor's public release
notes (contrast [[decisions]], which records *why*; this records *what* and *when*).
See [[roadmap]] for what's still ahead.

## Sprint 1 — 2026-08-06 to 2026-08-13

| Item | Notes | Source |
|---|---|---|
| Badge-event ingestion pipeline | End-to-end in staging by the Sprint 1 demo: consumes badge events from Daniel Osei's team's system, writes zone-access records. | [[meetings]] — Sprint 1 Review, 2026-08-13 |
| Sample record schema | Postgres schema for sample chain-of-custody (collection → transfer → disposal); no CRUD UI yet, data-model only this sprint. | [[meetings]] — Sprint 1 Planning, 2026-08-06 |
| Okta SSO spike | De-risked the Okta integration ahead of building real auth flows against it. | [[meetings]] — Sprint 1 Planning, 2026-08-06 |
| NestJS service scaffold, single service for both modules | `facility-access` and `sample-inventory` as modules within one service, per [[decisions]]. | [[decisions]] (tracked as [HIVE-41](https://linear.app/umbrella-corp/issue/HIVE-41)) |
| Fix: badge-event duplicate writes on retry (HIVE-47) | Retried badge events from the ingestion queue were being written twice under load; ingestion now keys on the badge system's own event ID. | (source: Granola note "Sprint 1 Review / Sprint 2 Planning", 2026-08-13; tracked as [HIVE-47](https://linear.app/umbrella-corp/issue/HIVE-47)) |

## Sprint 2 — 2026-08-13 to 2026-08-20

| Item | Notes | Source |
|---|---|---|
| Sample-record CRUD | Full create/read/update endpoints for sample records on top of the Sprint 1 schema; technicians can log collection/transfer/disposal events. | [[meetings]] — Sprint 1 Review / Sprint 2 Planning, 2026-08-13 |
| Audit log view | Read-only screen (`Audit Trail`) surfacing badge-access and sample-custody events in one timeline, ahead of Phase 2's formal export work. | [[meetings]] — Sprint 1 Review / Sprint 2 Planning, 2026-08-13 |
| Override-approval flow, design handoff | Ines Novak's designs for the override-request and approval screens (`Request Access Override`, `Pending Overrides`) handed to engineering; build lands after Sprint 2 review. | [[meetings]] — Sprint 1 Review / Sprint 2 Planning, 2026-08-13 |
| Override-approval record, API contract | `POST /overrides` / `PATCH /overrides/:id` contract locked ahead of the build, so it matches what Meridian & Cole confirmed the 2027 audit export will need. | [[decisions]] — audit export format sign-off, 2026-08-11 (tracked as [HIVE-58](https://linear.app/umbrella-corp/issue/HIVE-58)) |
| Nightly Oracle export, staging bucket read path | Hive OS's read side of the one-way nightly export from UMBRA's Oracle database, per the strangler-fig boundary. | [[architecture]] |
| Fix: sample-record timestamps stored in local site time, not UTC (HIVE-63) | Caught during Sprint 2 QA — chain-of-custody timestamps need to be unambiguous across the six research sites' time zones once the remaining sites cut over. | (source: Granola note "Sprint 1 Review / Sprint 2 Planning", 2026-08-13; tracked as [HIVE-63](https://linear.app/umbrella-corp/issue/HIVE-63)) |
| Sprint 2 review | Scheduled 2026-08-20; not yet held. This row will be confirmed against the review once it happens rather than assumed complete. | [[meetings]] — Sprint 2 Review / Sprint 3 Planning, 2026-08-20 *(scheduled)* |

## Notes

- This log is written by hand from the meeting and decision record, not synced from a
  CI/CD or release-tagging system — there isn't one configured yet (see
  [[stack]] §Infrastructure).
- Anything dated 2026-08-20 or later is provisional until the corresponding meeting
  actually happens; see [[meetings]].
