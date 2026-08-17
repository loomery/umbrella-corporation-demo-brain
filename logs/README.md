# Change log

One file per change session, named `YYYY-MM-DD-<short-slug>.md`. One file rather than one
shared append-only log, because this brain is shared through git and an append-only file
conflicts on every parallel edit. Date-prefixed names sort chronologically, so "read the
most recent entries" is a directory listing.

Git records which bytes changed. This records what the agent believed — where a claim came
from, what it assumed when a source was ambiguous, and what it knowingly left undone. That
is what the next session needs and what a diff cannot tell it.

Get the date by running `date`, never from memory.

## Format

```markdown
# 2026-01-15 — Onboarding phases 1–2

**Agent:** Claude Code (opus-5), via /onboard
**Changed:** sources.yaml, docs/engagement.md, docs/onboarding-status.md
**Grounded in:** Granola folder "Acme × Loomery" (3 meetings); LIN-142
**Assumed:** read "Q4" in the kickoff meeting as 2026-Q4 — unconfirmed
**Left open:** product-context.md domain notes — no source covers this, needs a human
```

`Assumed` and `Left open` are the fields that justify this file existing. If an entry has
neither, say so explicitly rather than dropping the headings.
