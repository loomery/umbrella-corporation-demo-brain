# Umbrella Corporation — Onboarding Procedure

This file is the single source of truth for taking this brain from empty scaffold to
something a colleague can query. `skills/onboard/SKILL.md` (and its `.claude`/`.agents`
mirrors) points here rather than duplicating this content.

Work through it as a conversation, not a batch job. Ask one question at a time and wait
for the answer; a person can correct a wrong assumption in a sentence, but only if you
gave them the chance before you acted on it.

## 1. Resume

Read [[docs/onboarding-status]], `sources.yaml`, `brain.config.json`, [[README|README.md]], and
the newest files in `logs/`. [[README|README.md]]'s MCP subsections carry the reasoning behind
each source's endpoint — including why a source may have none yet. Report what is done
and what is next in one screen. If nothing remains, say so and hand off to `/brain`.

Never re-ask something a previous run already recorded. If the status file answers a
question in §2, skip it and say what you already know instead — being asked twice is how
a brain loses someone's confidence.

## 2. Ask before you look

A fresh brain has no context. The fix for that is a conversation, not a search.

**Do not fan out across everything connected.** It is slow, it buries the useful in the
irrelevant, and — because user-level connectors are often authenticated against Loomery's
own workspace rather than the client's — it can reach other clients' material that is
none of this engagement's business. That is what `sources.yaml`'s `exclusions` is for.
One named source the user pointed you at beats ten you found by yourself.

So open by asking what they have. One question per message, in this order — each one
makes the next cheaper to answer:

1. **"In a sentence or two, what is this engagement?"** What Loomery is doing for
   Umbrella Corporation, and what phase it is in — pitch, discovery, delivery, support.
2. **"What have you got that I can read?"** Name the candidates rather than asking
   open-endedly: a proposal or SOW, a kickoff or discovery deck, meeting notes, a Slack
   channel, a Linear/Jira project, a Drive folder, a Miro board, an email chain. Ask them
   to paste it, drop it into `docs/inbox/`, or just tell you where it lives.
3. **"Which of these should I actually use?"** List the sources in `sources.yaml` beside
   the connectors you can see in this session, and ask which apply — and for each,
   whether it is the client's workspace or Loomery's. Do not resolve this by guessing;
   §3 shows how to confirm it.
4. **"Who are the people?"** Client-side and Loomery-side, and who decisions route
   through.
5. **"Anything I should stay out of?"** Channels, folders, or topics that are off-limits.
   Write the answer into `sources.yaml`'s `exclusions`.

If the answer is "you tell me", or you get nothing at all: do not treat that as
permission to search everything. Say plainly what you would otherwise be guessing at,
propose the narrowest useful first move — one named source, for one named purpose — and
get a yes before touching it.

Play back what you heard in a few lines before moving on, so a misheard detail gets
corrected now rather than propagating into every doc you write.

## 3. Wire the sources as pointers

Every source here is **the client's own workspace, not Loomery's** — the client's
Slack, the client's Linear, the client's Drive. Loomery's instances of the same tools
are out of scope, and `sources.yaml`'s `exclusions` says so.

For each source in `sources.yaml`: check `.mcp.json` before assuming anything is
missing — a source can be deliberately un-prewired because no confirmed endpoint exists
yet (Monday.com today; [[README|README.md]]'s MCP section says why), and that is not a setup gap
to fix by guessing. For everything else, probe whether its MCP tools are visible in this
session before assuming anything needs installing — many people have these connected
as user-level connectors already. **A visible connector is not automatically the right
one:** a user-level Slack or Drive connector is often authenticated against Loomery's
workspace, so confirm which workspace or account the tools actually reach before
recording it as wired. Call a cheap identifying tool (list workspaces, list teams,
whoami) and show the user what came back. If it is Loomery's rather than the client's,
that source needs a separate project-specific login — record it as auth-pending
against the client's instance rather than ticking it off.

Then ask for identifiers in human terms and resolve them live (call the source's own
list/search tool to turn "the Bite folder" into a real ID; never ask a person for a
UUID). Notion, Google Drive, Miro and Figma are index-style: `sources.yaml` has no
identifier slot for them, and their `docs/<key>.md` starts as an empty table. Once
wired, seed that table yourself — one pointer per row (name, what it covers, link or ID,
last checked) for each board, drive, space or file the client actually uses — never the
source's content itself. If a source is unused, delete its block from `sources.yaml` and
note the decision in the status file, so it is never re-asked.

Where an MCP has a confirmed endpoint but is absent, print the exact
`claude mcp add --transport http <name> <url>` line, record auth-pending, and move on.
Where no confirmed endpoint exists, ask the user to fetch the URL from the vendor's own
docs and record auth-pending — never guess one; a wrong URL fails at authentication with
no obvious cause, worse than printing nothing. Never block the whole run on one source.

Asked to add a tool this brain was not scaffolded for at all: mirror an existing
source's blocks as the template, across all six places a source is declared — its block
in `sources.yaml`, `.mcp.json`, and `opencode.json`; a routing row and a sync bullet in
`skills/brain/PLAYBOOK.md`; and an MCP subsection in [[README|README.md]]. If it behaves like an
index-style source, also create its `docs/<key>.md` with the same pointer table as the
others. Same rules throughout: identifiers resolved live, pointers not copies, propose
before writing anything.

## 4. Ground the docs, thin and cited

Read the wired sources. Draft a few sentences per `TODO(brain)` marker, each carrying
an anchor (meeting ID, channel, issue key, `file:line`). Present every draft in one
batch for approval before writing anything, per `brain.config.json`'s
`sync.proposeBeforeEdit`. Never paste source content in wholesale — the brain is a
router, and two copies of a fact diverge. Where a live source owns an answer outright,
write a routing line instead of prose.

Batch by document rather than dumping every draft at once: "here is what I propose for
[[docs/engagement]]" is reviewable, forty drafts across nine files is not. Take the
corrections and carry them into the next batch.

Uncited means unwritten: if no live source supports a claim, leave the marker in place and ask a human.

## 5. Interview the gaps

Only what no source can answer: commercial context, engagement dates, who decisions
route through, domain terminology. One question at a time.

Ask about the gap you actually hit, and say why you are asking — "nothing in the meetings
says who signs off on scope changes; who does?" gets a better answer than a bare
questionnaire. If they do not know either, that is a legitimate outcome: record it as
open rather than inventing a plausible answer.

## 6. Collect what MCPs cannot reach

Ask explicitly for email chains, the SOW, kickoff decks, whiteboard photos. Durable
material worth citing later goes in `docs/source-materials/` and may be cited from
committed docs; one-off material goes in `docs/inbox/`, is processed, and is never
cited from a committed doc. Record the outstanding ask in the status file so a later
run chases it.

## 7. Close out — show your work so it can be checked

Re-count `TODO(brain)` markers, update [[docs/onboarding-status]], write the `logs/`
entry, and offer to commit per `brain.config.json`'s `writeMode`.

Then print a handover the user can actually audit. The point is that they can skim it,
spot the one thing you got wrong or missed, and say so — a prose paragraph hides exactly
that. Print all three parts, even when a section would be empty; say "none" rather than
dropping the heading.

**What changed.** One row per file you touched, so every claim is traceable back to
where it came from:

| File | What changed | Grounded in | Check this |
|---|---|---|---|
| `docs/engagement.md` | Phase, scope, dates | Granola "Kickoff" 2026-01-15; SOW p2 | Dates were spoken, not written down |
| `sources.yaml` | Wired Slack + Drive | — | Drive folder ID resolved live, confirm it is the right folder |

`Check this` is the column that earns the table: name the specific thing you are least
sure of in that file, or leave it blank if you are confident. Do not write "please
review" — say what to look at and why.

**Sources.** One row per source in `sources.yaml`, including the ones that are not
working, since those are what a later run needs to chase:

| Source | Status | Points at | Notes |
|---|---|---|---|
| Granola | ✓ wired | client's workspace | 3 meetings read |
| Slack | △ auth-pending | Loomery's, needs client login | Connector reaches the wrong workspace |

**Still open.** Anything you assumed, could not verify, or deliberately left alone, and
anything you need from a human — with what it would unblock, so they can judge whether
it is worth their time. If a `TODO(brain)` marker is still there, it belongs in this
list, not in the "what changed" table.

Finish by asking whether anything is missing or wrong, and offer to correct it in the
same session. That is cheaper for everyone than a wrong fact reaching a client doc.

## Guardrails

- Ask before searching — never fan out across every connected tool to work out what this
  engagement is. A wide sweep reaches other clients' material and buries the useful.
- One question at a time, and never re-ask what the status file already answers.
- Pointers, not copies — never write source content into the brain wholesale.
- Every claim anchored — no fabrication, cite a source or omit.
- Batch-propose changes for approval before writing them.
- Refuse to write credentials into the brain even if a pasted email chain contains
  them, and say why.
- Only the shared folders and channels named in `sources.yaml` — never private
  messages or other clients' spaces.
- No local filesystem paths in shared docs.
- Explicit approval before commit or push.
