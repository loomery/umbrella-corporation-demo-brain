# 2026-08-17 — Demo onboarding (fictional client)

**Agent:** Claude Code (Sonnet 5), via /onboard
**Changed:** sources.yaml; docs/engagement.md, stakeholders.md, meetings.md,
product-context.md, technical/stack.md, technical/decisions.md, onboarding-status.md;
README.md; AGENTS.md
**Grounded in:** nothing real — Umbrella Corporation is a fictional client, requested
explicitly by the user as a demo of the project-brain tooling. All "(source: ...)"
citations in the docs above point at fabricated Granola notes, Slack messages, and
Drive files that do not exist. `sources.yaml` marks every source `simulated`.
**Assumed:** everything — company (multinational pharma/consumer health, HQ Raccoon
City), engagement (replacing legacy UMBRA with new Hive OS platform), phase (Delivery,
Phase 1, Sprint 2), all named people, dates, and technical decisions were invented to
be internally consistent with each other and with the other project brains' voice
(Secret Escapes, Eque2-Chalkstring), not derived from any source. Deliberately did not
run the normal §2 "ask before you look" interview from `skills/onboard/ONBOARDING.md`,
since there is no real person or source to interview.
**Left open:** if this brain is ever repurposed for a real client, every doc under
`docs/` needs to be rewritten from scratch via a proper `/onboard` run — none of this
content should survive that transition. `src/` has no submodule (no real code to add
for a fictional client). Frontend (`.brain-site`) set up and built in this same
session — see the immediately following log entry / commit for that.
