---
title: "Meetings"
audience: [internal]
roles: [engineering, product, design]
onboarding:
  order: 3
  prerequisites: [engagement]
  summary: The meeting log, in date order, underpinning the engagement timeline
  estimate: 5m
status: current
owner: tom@loomery.com
updated: 2026-08-17
---

> **Demo brain.** Simulated meeting log for a fictional client — see
> [[onboarding-status]]. No live Granola folder is connected; these rows were
> written by hand during onboarding to demonstrate the sync format.

# Meetings

One-paragraph purpose: the meeting log synced from Granola. The sync routine appends
rows to the table below — do not reformat it by hand.

| Date | Title | Attendees | Transcript / Notes |
|---|---|---|---|
| 2026-05-20 | SOW Sign-Off Call | Patrick Bishop, Brett Thornton, Sarah Chen, Marcus Webb | [Granola note](https://notes.granola.ai/d/a3f7c2e1-9b4d-4e6a-8f21-5c7d9e0b1a34) — Umbrella confirms scope: replace UMBRA with Hive OS, Phase 1 = Facility Access + Sample Inventory. SOW signed same day. |
| 2026-06-15 | Kickoff | Brett Thornton, Milly Allatson, Tom Holmes, Sarah Chen, Grace Kowalski, Marcus Webb | [Granola note](https://notes.granola.ai/d/b8e2d915-3c6f-4a1b-9d84-2f5e7c8b0a63) — Introductions, engagement cadence agreed (2-week sprints, Mon/Thu syncs), Discovery scheduled for late June/July. |
| 2026-07-02 | Discovery: Facility Access Workflows | Tom Holmes, Milly Allatson, Marcus Webb, Daniel Osei | [Granola note](https://notes.granola.ai/d/c4a91f7e-6d3b-4c8a-b2f1-8e9d0a5c7b12) — Walked current badge-and-override process in UMBRA; identified the manual-override log as the weakest audit point. |
| 2026-07-16 | Discovery: Sample Inventory & Compliance Reporting | Tom Holmes, Milly Allatson, Priya Anand, Marcus Webb | [Granola note](https://notes.granola.ai/d/d716e8b3-2f4a-4d9c-a5e7-1b8c6d0f3a92) — Priya flagged chain-of-custody reconstruction as the hard requirement for the 2027 FDA audit cycle. |
| 2026-07-30 | Phase 1 Scope Review | Brett Thornton, Milly Allatson, Sarah Chen, Priya Anand, Grace Kowalski | [Granola note](https://notes.granola.ai/d/e2c8a4f1-7b9d-4e3c-8a6f-0d5b1e7c9a48) — Phase 1 scope locked: Facility Access & Sample Inventory. Success metrics agreed (see [[engagement]]); recap posted to [Slack](https://umbrellacorp.slack.com/archives/C05U8K3QXTN/p1722345678000123). |
| 2026-08-06 | Sprint 1 Planning | Milly Allatson, Tom Holmes, Grace Kowalski, Daniel Osei | [Granola note](https://notes.granola.ai/d/f9b3d6e2-4a8c-4f1b-9e7d-3c0a5b8f2d61) — Sprint 1 backlog set: badge-event ingestion, sample record schema, Okta SSO spike. |
| 2026-08-11 | Audit Readiness Sync | Priya Anand, Trevor Lindqvist (Meridian & Cole), Tom Holmes | [Granola note](https://notes.granola.ai/d/a1d5e9c3-8f6b-4a2d-b7e4-6c9f0a3d5b18) — External auditor walked through what the 2027 FDA cycle will expect from a digital chain-of-custody export; confirmed the override-approval record design covers it. |
| 2026-08-13 | Sprint 1 Review / Sprint 2 Planning | Milly Allatson, Tom Holmes, Grace Kowalski, Daniel Osei, Ines Novak | [Granola note](https://notes.granola.ai/d/b6f2a8d4-3e9c-4b7a-8d1f-5a2e7c9b0f36) — Sprint 1 demo: badge-event ingestion pipeline working end-to-end in staging. Sprint 2 adds sample-record CRUD + audit log view; Ines joins to design the override-approval and audit-export screens. |
| 2026-08-14 | Group Steering Committee — Q3 Review | Robert Kaine, Wendy Ashford, Sarah Chen, Brett Thornton | [Granola note](https://notes.granola.ai/d/c3e7b1f9-6a4d-4c8e-9b2f-7d0a5c8e3b41) — Group-level check-in. Kaine confirmed Phase 1 budget is on track; Ashford flagged interest in Hive OS as a template for Umbrella Pharmaceuticals' and Consumer Health's own legacy plant-ops systems, contingent on a clean Raccoon City cutover. |
| 2026-08-20 *(scheduled)* | Sprint 2 Review / Sprint 3 Planning | Milly Allatson, Tom Holmes, Grace Kowalski, Daniel Osei | Not yet held, no transcript yet. Sprint 2 scope: sample-record CRUD, audit log view, override-approval flow design handoff from Ines. |
