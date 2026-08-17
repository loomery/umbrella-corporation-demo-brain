---
title: "Glossary"
audience: [internal]
roles: [engineering, product, design]
onboarding:
  order: 3
  prerequisites: [engagement]
  summary: Domain terms this brain assumes — Hive OS, UMBRA, chain-of-custody, and the rest
  estimate: 3m
status: current
owner: tom@loomery.com
updated: 2026-08-17
---

> **Demo brain.** Simulated glossary for a fictional client — see
> [[onboarding-status]].

# Glossary

One-paragraph purpose: the domain vocabulary used across this brain, so a new reader
doesn't have to reconstruct it from context on their first pass through
[[product-context]] or [[decisions]].

- **Hive OS** — the new platform Loomery is building; see [[product-context]].
- **UMBRA** — the legacy VB.NET/Oracle system Hive OS replaces, running independently
  at each of Umbrella's six research sites; see [[stack]].
- **Chain-of-custody** — the reconstructable record of a sample's collection, transfer,
  and disposal; the hard requirement behind most Phase 1 design decisions, see
  [[decisions]].
- **Manual override** — a technician granted temporary access outside their normal zone
  permissions; today logged on paper, made a first-class record in Hive OS; see
  [[product-context]] and [[architecture]].
- **Strangler-fig migration** — cutting over one research site at a time rather than
  globally; see [[decisions]].
- **One Hive** — Umbrella's internal name for consolidating the six sites' independent
  UMBRA instances onto a single platform; see [[engagement]].
- **Applied Biosciences** — the Umbrella division this engagement is with, one of three
  alongside Umbrella Pharmaceuticals and Umbrella Consumer Health; see
  [[product-context]] and [[stakeholders]].
