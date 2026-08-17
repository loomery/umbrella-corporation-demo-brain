---
title: "Product Context"
audience: [internal]
roles: [engineering, product, design]
onboarding:
  order: 3
  prerequisites: [engagement]
  summary: What Hive OS replaces, who uses it, and the compliance domain vocabulary
  estimate: 10m
status: current
owner: tom@loomery.com
updated: 2026-08-17
---

> **Demo brain.** Simulated product for a fictional client — see
> [[onboarding-status]].

# Product Context

One-paragraph purpose: what Umbrella Corporation the product does, who its users are, and
the domain knowledge an AI session needs before reasoning about feature work.

## Company background

Founded in 1968 as an agrochemical business, Umbrella Corporation diversified into
pharmaceuticals through the 1980s and now operates as a group of three divisions:
**Applied Biosciences** (R&D labs, the subject of this engagement), **Umbrella
Pharmaceuticals**, and **Umbrella Consumer Health**. Group headquarters are in Raccoon
City; Applied Biosciences runs six research sites — Raccoon City, Barcelona, Osaka,
Cape Town, Vancouver, and Warsaw — each historically operating with a good deal of
local autonomy over its own tooling, which is exactly why UMBRA ended up as six
independently-customised instances rather than one shared system. Umbrella is a
public company (mid-cap, listed) with roughly 14,000 employees group-wide; Applied
Biosciences is the smallest of the three divisions by headcount. (source: Google
Drive, "Umbrella × Loomery — SOW v1.2"; Granola note "Kickoff", 2026-06-15)

Each division runs its own operational systems independently, but Hive OS is being
watched at group level as a possible template for the other two divisions' own legacy
plant-ops software — see [[engagement]] §Group interest. (source: Granola note
"Group Steering Committee — Q3 Review", 2026-08-14)

## What it does

**Hive OS** is a lab-operations platform for Umbrella's Applied Biosciences division. It
replaces **UMBRA**, an on-prem VB.NET/Oracle system running since 2003 at each of
Umbrella's six research sites independently, with a single hosted platform covering
three areas: facility access (badge issuance, zone-level permissions, override
approvals), sample inventory (chain-of-custody from collection through disposal), and
compliance reporting (audit-ready exports for regulators). Phase 1 covers facility
access and sample inventory; compliance reporting is Phase 2. (source: [Google Drive](https://drive.google.com/file/d/1A9nB3vQeXyZpR7mK2dF8hLtC5wS4oJq6/view),
"Umbrella × Loomery — SOW v1.2"; Granola note "Phase 1 Scope Review", 2026-07-30)

## Users

- **Lab technicians** — log sample collection/transfer/disposal events throughout the
  day; need this to be fast enough not to interrupt bench work.
- **Facility security staff** — issue and review badge access, action override requests
  when a technician needs zone access outside their normal permissions.
- **Compliance & Quality (Priya Anand's team)** — pull audit-ready chain-of-custody and
  access reports ahead of inspections; today this means manually reconciling paper
  override logs against UMBRA exports, which is the exact gap Hive OS closes.
(source: Granola notes, "Discovery: Facility Access Workflows" 2026-07-02 and
"Discovery: Sample Inventory & Compliance Reporting" 2026-07-16)

## Domain notes

See [[glossary]] for quick definitions of the terms below.

- **Chain-of-custody** must be reconstructable from the system alone with zero paper
  backstops — this is the hard requirement behind most Phase 1 design decisions (see
  [[decisions]]).
- **Manual overrides** (a technician granted temporary access outside their normal
  zone permissions) are today logged on paper at each site and are the single weakest
  point in Umbrella's current audit trail. Hive OS makes every override a first-class,
  timestamped record.
- **Site independence**: each of the six research sites currently runs its own UMBRA
  instance with site-specific customisations, which is why the migration is
  strangler-fig (site-by-site) rather than a single global cutover — see
  [[decisions]].
- **Raccoon City pilot site** is the first cutover target, chosen because it's the
  smallest site by headcount and shares a facilities team with the compliance office,
  making rollback verification easier. (source: Granola note "Phase 1 Scope Review",
  2026-07-30)
