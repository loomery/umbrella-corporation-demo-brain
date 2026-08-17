# 2026-08-17 — Graph view demo, role onboarding, more background

**Agent:** Claude Code (Sonnet 5), continuing the demo-onboarding session
**Changed:** docs/glossary.md (new), docs/technical/architecture.md (new),
docs/technical/roadmap.md (new); frontmatter (`audience`, `roles`, `onboarding`) added
to engagement.md, stakeholders.md, meetings.md, product-context.md, onboarding-status.md,
technical/context.md, technical/stack.md, technical/decisions.md; company-background
section added to product-context.md; group-level stakeholders (Group CFO, Group CIO,
external auditor) added to stakeholders.md, engagement.md, dashboard.yaml,
dashboard.status.yaml; brain-site.yaml pageTitle shortened to "Umbrella Brain"
**Grounded in:** nothing real — same demo-brain caveat as the initial onboarding; all
citations are fabricated
**Assumed:** role taxonomy for onboarding paths (engineering/product/design), matching
Eque2-Chalkstring's convention (`roles` + `onboarding.prerequisites/order/summary/estimate`
frontmatter, consumed by the shared `@loomery/brain-site` onboarding-emitter plugin)
**Fixed:** every internal wikilink in `docs/*.md` used a `docs/`-prefixed target (e.g.
`[[docs/engagement]]`) copied from AGENTS.md's convention for linking *into* the docs
tree from outside it (README.md, AGENTS.md) — wrong for links *within* the docs tree
itself, where Quartz resolves bare filenames (`[[engagement]]`). This silently broke
every cross-doc link (rendered as `/docs/<slug>`, a 404) and would have made the graph
view and backlinks panels show nothing. Stripped the `docs/` and `docs/technical/`
prefixes across all of `docs/`; `npx brain-site validate` now reports 0 errors and
backlinks/graph render correctly.
**Left open:** graph view currently renders as one connected chain rather than visually
separate clusters — the doc set is small enough and prerequisite-linked heavily enough
that force-directed layout doesn't visually separate technical vs. engagement docs into
distinct blobs, though the connectivity itself (backlinks, onboarding paths) is correct.
Would need a larger, more compartmentalised doc set to show dramatic visual clustering.
Left the real Resident Evil "Umbrella Corporation" logo file
(`assets/static/umbrella-logo.svg`) as the user set it, against this agent's own
recommendation — see chat history for the reasoning; did not revert per explicit user
instruction not to touch it.
