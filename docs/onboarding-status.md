---
title: "Onboarding Status"
audience: [internal]
status: current
owner: tom@loomery.com
updated: 2026-08-17
---

# Onboarding status

One-paragraph purpose: where onboarding got to on the Umbrella Corporation brain. `/onboard`
reads and updates this file, so a run that stops part-way resumes rather than repeats.
It is also the handover note: anyone picking this brain up can see what is grounded,
what was assumed, and what is still missing.

Notation: `✓` done · `△` partial · `✗` not started

## Demo disclosure

**This is a demo brain, not a real engagement.** Umbrella Corporation was requested
explicitly as a fictional client, so this run of `/onboard` did not follow its normal
"ask before you look" interview — there was no real person to interview and no real
sources to wire. Instead it fabricated a complete, internally-consistent engagement
(company, product, people, meetings, tech stack, decisions) in the same cited style a
real brain uses, so the tooling — routing, cross-links, the freshness check, the
frontend — can be demonstrated end to end.

Every "(source: ...)" citation in `docs/` points at a *simulated* Granola note, Slack
message, or Drive file — none of it is real, and none of it is wired to a live MCP
connector. `sources.yaml` marks every source `status: simulated` for this reason. A
real `/onboard` run would never fabricate content this way — see
`skills/onboard/ONBOARDING.md` §2 ("ask before you look") and the guardrails at the
end of that file, which this run deliberately set aside only because the client itself
is fictional and the user asked for a populated demo.

## Sources

All four sources in `sources.yaml` (Granola, Slack, Linear, Google Drive) are
`simulated` — there is nothing to wire, since there is no real Umbrella Corporation
workspace to connect to.

## Docs

- `docs/engagement.md` — ✓ done (simulated)
- `docs/stakeholders.md` — ✓ done (simulated)
- `docs/product-context.md` — ✓ done (simulated)
- `docs/technical/` — ✓ done (simulated); `src/` intentionally has no submodule — see
  `src/README.md` and `docs/technical/stack.md`
- `docs/meetings.md` — ✓ done (simulated, 7 rows)

## Waiting on a human

Nothing — this is a closed demo dataset, not a live engagement with open threads.

If this brain is ever repurposed for a *real* client, everything under `docs/` should
be treated as scratch and rewritten from scratch via a proper `/onboard` interview
before anyone relies on it.
