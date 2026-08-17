---
name: onboard
description: >-
  First-run setup for the Umbrella Corporation brain. Use when this brain is new or still
  has TODO(brain) markers, when asked to set up, onboard, initialise, or fill in the
  brain, when connecting sources or MCP servers for the first time, or when asked what
  is still missing before the brain is usable.
---

# Onboard the Umbrella Corporation brain

This brain is a skeleton until its sources are wired and its docs are grounded. This
skill takes it from scaffold to something a colleague can query, as a conversation: it
asks what the user already has — documents, accounts, which connectors point at the
client rather than Loomery — instead of searching everything connected to find out. It
closes with a table of every file it touched and what to double-check in each.

`ONBOARDING.md` sits in this skill's own directory, alongside this file. Read it and
follow it in full; it is the procedure, and this file only routes to it. Read it as a
sibling of this file — never as the bare path `brain/ONBOARDING.md`, which resolves
against whatever directory the agent happens to be running in.

Every step of onboarding is a write, so unlike `/brain` it has no useful read-only mode.
Check you can write before starting.

If there is no filesystem to walk, and so no `brain.config.json` anywhere — as in Claude
in chat, which carries this skill but not the repo — stop and say so. Onboarding cannot
run here at all: there is nowhere to put anything. Don't improvise a substitute, don't
interview the user to rebuild the brain's content in the conversation, and don't call the
brain broken; it isn't. Tell them to open this brain in Claude Code, Codex CLI or
opencode and run `/onboard` there. `/brain` still works here, read-only, in the
connector-only mode its playbook describes.

Otherwise run §0 ("Establish the brain") from `../brain/PLAYBOOK.md` first,
unconditionally — the filesystem exists in that case, so reading the sibling skill's
resource resolves fine. If §0 lands on its read-only fallback (step 4), stop there too
and say onboarding needs a real checkout, rather than producing nothing read-only.

Onboarding is resumable — [[docs/onboarding-status]] records where you got to, so
starting again after a break or an MCP restart picks up rather than repeating.

Once onboarding is complete, `/brain` takes over for day-to-day use and `/brain sync`
keeps it current.
