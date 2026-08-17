---
title: "Decisions"
audience: [internal]
roles: [engineering, product]
onboarding:
  order: 6
  prerequisites: [technical/context]
  summary: Significant technical decisions and why they were made
  estimate: 5m
status: current
owner: tom@loomery.com
updated: 2026-08-17
---

> **Demo brain.** Simulated decisions for a fictional client — see
> [[onboarding-status]].

# Decisions

One-paragraph purpose: a log of significant technical decisions on Umbrella Corporation and
why they were made, so an AI session doesn't re-litigate settled questions. See
[[architecture]] for how these decisions shape the current system, and
[[roadmap]] for what's deferred rather than decided against.

See [[changelog]] for when each of these decisions actually landed in shipped work.

## Log

### Strangler-fig migration, not a big-bang cutover — 2026-07-02

Each of Umbrella's six research sites runs its own independently-customised UMBRA
instance. A single global cutover would mean validating all six at once against
Priya Anand's audit-trail requirement, with no fallback if one site's data doesn't
migrate cleanly. Agreed instead to cut over site-by-site, starting with Raccoon City
(smallest site, shares a facilities team with the compliance office). UMBRA keeps
running at not-yet-migrated sites throughout. (source: Granola note "Discovery:
Facility Access Workflows", 2026-07-02)

### PostgreSQL over Oracle for Hive OS's own data — 2026-07-16

UMBRA's Oracle 11g licence is tied to Umbrella's legacy support contract, which
Umbrella wants to exit as sites migrate off UMBRA. New data goes straight into
PostgreSQL on RDS rather than a new Oracle schema; the nightly batch export from
Oracle is a one-way read during the migration window only; nothing new is written back
to Oracle. (source: Granola note "Discovery: Sample Inventory & Compliance Reporting",
2026-07-16)

### Every manual override is a first-class, timestamped record — 2026-07-30

The single biggest audit-trail gap in UMBRA is that facility-access overrides are
logged on paper at each site rather than in the system. Hive OS makes an override
request and its approval/denial a normal database row from day one of Phase 1, rather
than a fast-follow — Priya Anand's team made this a condition of scope sign-off.
(source: Granola note "Phase 1 Scope Review", 2026-07-30)

### Audit export format signed off with the external auditor, not guessed internally — 2026-08-11

Rather than designing the compliance export against Priya Anand's team's own
interpretation of FDA expectations, Meridian & Cole (the external audit firm) reviewed
the override-approval record design directly and confirmed it covers what a 2027
inspection will ask for: who requested access, who approved it, and a timestamp trail
with no manual/paper step in between. Avoids redesigning the export later against a
requirement nobody outside Compliance had actually validated. (source: Granola note
"Audit Readiness Sync", 2026-08-11; tracked as
[HIVE-58](https://linear.app/umbrella-corp/issue/HIVE-58))

### One NestJS service for both Phase 1 modules, not two — 2026-08-06

Facility Access and Sample Inventory are built as modules inside a single NestJS
service rather than separate microservices, since both are small, share the same
Postgres database and Okta auth, and splitting them now would add deployment overhead
with no team large enough yet to need the isolation. Revisit if Phase 2 (compliance
reporting) turns out to need independent scaling. (source: Granola note "Sprint 1
Planning", 2026-08-06; tracked as
[HIVE-41](https://linear.app/umbrella-corp/issue/HIVE-41))
