---
name: brain
description: >-
  Umbrella Corporation project brain — orientation, routing, and sync. Invoke BEFORE
  answering any question about Umbrella Corporation, its product, people, code, meetings,
  or delivery status; also when asked to sync/ingest the latest context
  ("/brain sync"), or when writing anything back to the project's live tools.
---

# Umbrella Corporation brain

This repo is a routing and augmentation layer, not the source of truth: `sources.yaml`
points at the live systems that are. Always ground answers in a live source and cite
anchors (file:line, meeting IDs, issue keys, board/widget IDs) so claims are traceable.

## Read the playbook — it travels with this skill

`PLAYBOOK.md` sits in this skill's own directory, alongside this file. Read it: it is
the map of this repo and its live sources, and it defines both the default orientation
mode and the sync routine.

Because it is a resource of this skill rather than a file elsewhere in the repo, it
comes with the skill everywhere the skill goes — including environments that have no
filesystem and no checkout at all, such as Claude in chat, where the repo around the
skill is simply not present. Read it as a sibling of this file; never as the bare path
`brain/PLAYBOOK.md`, which resolves against whatever directory the agent happens to be
running in.

Run the playbook's §0 ("Establish the brain") first, unconditionally, before dispatching
to either mode — not only when the argument is `sync`. A bare `/brain` can just as
easily be running against a bundled snapshot, or against no filesystem whatsoever, as
against a real checkout, and §0 is what tells you which.

Then, if §0 established a writable checkout: with the argument `sync`, run the
playbook's sync procedure (§4) in full; otherwise run its default orientation mode (§3).
If `TODO(brain)` markers remain, say so and point to `/onboard` rather than working
through them here.

The freshness check in §3 step 2 runs on every invocation, including when someone asks a
direct question rather than requesting a sync. Answering first and checking later is the
one thing this skill must not do: the docs here are a cache, and a stale answer delivered
confidently is worse than a slow one.

## When there is no checkout at all

If §0 reaches its step 5 — no filesystem, so not even a bundled snapshot to fall back on
— you are in connector-only mode. Follow the playbook's routing table as normal, since
you can read it, but note what is and isn't possible:

- **Do not report this brain as missing, broken, or not set up.** It is not. You are in
  an environment that carries the skill but not the repo, which is expected. Say that
  plainly instead, in one line, so the person knows what they are getting.
- **You can still do the brain's actual job.** Its own first principle is that it routes
  to live sources rather than being the truth itself, and those sources are MCP
  connectors, not files. Route by the playbook's table and answer from them directly.
- **Ground every claim and cite an anchor** — meeting IDs, issue keys, message
  permalinks, document titles. With no cached docs to fall back on, an uncited claim is
  just a guess. If a connector is unavailable here, name the source you could not reach
  rather than answering from memory.
- **Refuse all writes.** No doc edits, no commits, no log entries, no `TODO(brain)`
  resolutions — there is nowhere to put them. If asked to sync or write back, say that
  `/brain sync` and `/onboard` need a real checkout, and point at Claude Code, Codex CLI
  or opencode opened on this brain.
- **Stay strictly within the playbook's routing table.** `sources.yaml` carries scoping
  rules — which channel, which Drive folder — that are not visible in this mode, so do
  not browse beyond what the table names.
