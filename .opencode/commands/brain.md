---
description: >-
  Umbrella Corporation project brain — orientation, routing, and sync. Run before
  answering any question about Umbrella Corporation; use the `sync` argument to run the
  ingest routine.
---

Read `skills/brain/PLAYBOOK.md` and follow it — it is the map of this repo and its live
sources.

If invoked with the argument `sync` ($ARGUMENTS is `sync`), run the playbook's `sync`
procedure (section 4) in full — which begins by running the playbook's §0 ("Establish
the brain") to establish a writable checkout before making any edits.

Otherwise, run the playbook's default orientation mode (section 3).
