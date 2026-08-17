---
title: "Architecture"
audience: [internal]
roles: [engineering]
onboarding:
  order: 4
  prerequisites: [technical/context]
  summary: How Hive OS and legacy UMBRA fit together during the strangler-fig migration
  estimate: 5m
status: current
owner: tom@loomery.com
updated: 2026-08-17
---

> **Demo brain.** Simulated architecture for a fictional client — see
> [[onboarding-status]].

# Architecture

One-paragraph purpose: how Hive OS and legacy UMBRA coexist during the migration, at a
level a new engineer can hold in their head before opening [[stack]].

## Shape, today

Hive OS runs as a single NestJS service (see [[decisions]] — one service,
not two, for Phase 1) against its own Postgres database, fronted by a React app and
sitting behind Okta SSO. It does not talk to UMBRA's Oracle database directly: Marcus
Webb's team runs a nightly batch export from Oracle into a staging bucket, and Hive OS
reads from that bucket rather than the live legacy system. Nothing flows back the other
way — the export is one-way for the length of the migration. (source: Granola notes,
"Discovery: Facility Access Workflows" 2026-07-02 and "Sprint 1 Planning" 2026-08-06)

## Why this shape

The nightly-export boundary exists because UMBRA has no API layer to integrate against
(it's a WinForms client talking straight to Oracle), and because the migration is
site-by-site rather than global — see [[decisions]] for the strangler-fig
rationale. Each research site cuts over independently; until it does, its UMBRA instance
keeps running unmodified and Hive OS's only view of it is that nightly export.

## What's deliberately out of scope here

Badge-hardware integration (the physical access-control system that emits badge
events) sits on Umbrella's side, owned by Daniel Osei's team — Hive OS only consumes
those events, it doesn't manage the badge readers themselves. See
[[roadmap]] for what's planned once Phase 1 ships.
