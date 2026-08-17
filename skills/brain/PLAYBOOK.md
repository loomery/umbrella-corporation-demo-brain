# Umbrella Corporation — Brain Playbook

This file is the single source of truth for how any AI session uses this repo. Every
agent adapter (Claude skill, opencode command, Codex prompt, `AGENTS.md`) points here
rather than duplicating this content.

## 0. Establish the brain

This runs before anything else, in either mode below (§3 or §4). This file and its
adapters (the Claude skill, the opencode command, the Codex prompt) are instructions
only, and the copy they were read from may not be a writable checkout at all — it may
be a read-only snapshot bundled inside a plugin cache. Never write into wherever this
playbook happened to be loaded from.

This file lives in the invoking skill's own directory (`skills/brain/PLAYBOOK.md`, or
`skills/onboard/ONBOARDING.md` for `/onboard`), as a resource of that skill. That is why
you can read it at all in environments that have no repo and no filesystem — it travels
with the skill. It does not follow that the rest of the brain travelled with it.

The harness supplies the invoking skill's own absolute install location on invocation
(Claude Code announces it as `Base directory for this skill: <path>`; other harnesses
give an equivalent). **The brain root is the nearest ancestor of that base directory
that contains a `brain.config.json`.** Walk upwards from the base directory until you
find one, and use that directory. Do not count directory levels: `../../` happens to be
right in both the in-repo layout (where `skills/` is reached through a symlink) and the
plugin-cache layout, but a fixed count is fragile — a shell `cd ../..` resolves the path
textually while a direct file read resolves it through the real filesystem, so the two
can disagree. Searching for the marker file cannot disagree with itself.

If you find one, read that `<brain root>/brain.config.json` to learn this brain's `slug`
and git `remote`. If there is no filesystem to walk at all — no way to list directories
or read files by path, as in Claude in chat — skip straight to step 5.

Then resolve a writable checkout, in order:

1. **Current tree.** If the working directory, or a parent of it, has a
   `brain.config.json` whose `slug` matches, or a matching git remote, use it — that
   directory *is* the brain root for the rest of this run, in place of whatever the base
   directory search above found. This is the ordinary case when already working inside
   the brain, and behaves exactly as it does today: reading and writing the working
   directory's own files is not just allowed here, it is the point. The ban above is on
   writing into the *bundled* copy, not on using a real checkout you are already sitting
   in.
2. **Remembered path.** If a checkout path was recorded on an earlier run, and it still
   exists on disk and its `brain.config.json` still has the matching `slug`, use it
   without asking again. The record lives at exactly
   `~/.warp-brain/<slug>/checkout-path.txt` — a single line holding an absolute path.
   Create the directory if it is missing, and write that file whenever step 1 or step 3
   establishes a checkout. This location is deliberately outside any harness's own
   plugin storage: Claude Code has a per-plugin data directory, but Codex and opencode
   have none, and a path that only works in one harness would leave the others
   re-resolving from scratch every time. It is also stated literally rather than as a
   variable on purpose — harnesses expand plugin-directory placeholders only inside
   hook, MCP-server, and monitor command strings, never inside prose like this, so a
   variable name written here would never resolve.
3. **Conventional locations, then clone.** Check the two locations this brain's own
   generator scaffolds into: `~/Documents/Project Brains/Umbrella Corporation` (the
   default) and `~/Developer/Project Brains/Umbrella Corporation` (the opt-in
   alternative) — both keyed on the project name, not the slug. If one exists and its
   slug matches, use it and record the path per step 2. Otherwise, if `remote` is
   known, offer to clone it to the first location and record the result. If `remote` is
   absent, try `git remote get-url origin` inside the bundled snapshot before giving up
   — the plugin cache is built from a clone, so an `origin` may well be set there. It
   may not be available, so treat a failure or empty result as normal, not an error. If
   that yields nothing either, ask for a checkout path rather than guessing one.
4. **Degraded fallback.** If no checkout can be established — cloning is declined, the
   machine is offline, git is unavailable — continue **read-only, from this bundled
   snapshot**, and say so explicitly and up front: state plainly that this is a frozen
   snapshot, not the live brain, and name the version it was built at, which is the last
   path segment of the **brain root** found above (not of the base directory, whose last
   segment is just the skill's own name). Depending on the harness that segment is
   either a git commit SHA or a pinned version string — report it verbatim, as "this
   snapshot's identifier", without claiming it is a commit SHA. Refuse every write — no
   doc edits, no commits, no log entries — until a real checkout exists. This is a hard
   requirement, not a nicety: a brain that answers confidently from a stale snapshot
   without saying so is the exact failure this design exists to prevent.
5. **Connector-only.** If there is no filesystem at all — not even a bundled snapshot to
   read, because nothing but this skill's own directory travelled here — then the routing
   table in §2 is still valid and the live sources it names are still reachable, because
   they are MCP connectors rather than files. Work from those directly. Say in one line
   that you are answering from live sources without this brain's cached docs, and that
   nothing can be written back. Do not describe the brain as missing, broken or not set
   up: it is not, and saying so sends people looking for a problem that does not exist.
   Every write rule in step 4 applies here too, for the same reason — there is nowhere to
   put them. `/brain sync` and `/onboard` need a real checkout; point at Claude Code,
   Codex CLI or opencode opened on this brain. Do not offer to open the brain as a
   website here either: there is no checkout to serve, and the offer would only
   mislead.

Once a checkout is established (steps 1–3), run `git pull --ff-only` in it, and target
every subsequent read and write there — never at wherever this playbook was loaded
from. The bundled copy is only ever a bootstrap. If that pull fails — a diverged branch,
uncommitted local changes, no network — say so and name the reason before continuing,
rather than working silently from a real-but-stale checkout; the user needs to know
whether they are looking at current context or yesterday's.

## 1. Operating principle

This repo is a routing and augmentation layer, not the source of truth: the live
systems in `sources.yaml` are truth, this repo is cache. Always ground answers in a
live source before answering a substantive question. Cite anchors — file:line, meeting
IDs, issue keys, board/widget IDs — so every claim is traceable back to where it came
from.

## 2. The map

```
umbrella-corporation-brain/
├── sources.yaml           # machine-readable source registry — start here
├── brain.config.json      # writeMode (push|pr) and sync behaviour
├── docs/meetings.md       # Granola meeting log (table, sync target)
├── docs/stakeholders.md   # who's who
├── docs/technical/        # index (context.md) + stack.md + decisions.md
└── src/                   # client code as git submodules — check technical/stack.md
                           # first, then `git submodule update --init` if empty
```

Routing table — topic → primary source → how to access:

| Topic | Primary source | Access |
|---|---|---|
| Client source code | (git submodules) | check `docs/technical/stack.md`, then browse `src/<RepoName>` |

## 3. Default mode — orient

On invocation with no arguments:
1. Run §0 above to establish the brain.
2. **Run the freshness check before answering anything.** Work through §4's source list
   and compare each live source against what the docs currently reflect. This is not
   optional, and a direct question is not a reason to skip it — an answer drawn from a
   stale cache is wrong in exactly the way this brain exists to prevent.
   - If nothing is new, say so in one line and carry on.
   - If something is new, summarise it in one message and ask whether to fold it in
     before answering. If they would rather have the answer first, give it — but say
     which parts rest on unsynced docs.
   - If a source is unreachable, name it. Silence from a source is not "nothing new".
3. Read `sources.yaml`, `brain.config.json`, and the Quick Facts in `CLAUDE.md`/`AGENTS.md`.
4. Report a one-screen orientation: what this project is, what's fresh vs. stale, and
   any `TODO(brain)` markers still open. If §0 landed on its degraded fallback, lead
   with that rather than burying it.
5. Offer the routine tasks below (sync, or answering a specific question) — noting
   that sync isn't available until a real checkout exists.
6. **Offer to open the brain as a website.** Check whether this checkout has both a
   `brain-site.yaml` and a `package.json` naming `@loomery/brain-site`. If it does, the
   frontend is available — ask, in one line:

   > Do you want me to open this brain as a website you can browse?

   If yes: run `npm i` (only needed the first time, and it may take a minute), then
   `npx brain-site serve`, and give them the link — `http://localhost:8080`. Say that
   edits to the docs show up on a refresh, and that it runs on their machine only, so
   nobody else can see it. Do not mention npm, Quartz, dev servers, ports or builds
   unless they ask — the offer and the answer should both make sense to someone who has
   never used a terminal.

   If those two files are absent, say nothing about a website. Do not offer to set one
   up as part of orientation; that is a change to their repo, not an answer to their
   question.

## 4. `sync` mode (`/brain sync`)

Run §0 above first. If it lands on the degraded fallback (step 4), stop here rather
than continuing: sync exists to write back to live sources, and §0 refuses every write
until a real checkout is established — explain that to the user instead.

Then, for each source in `sources.yaml`:

- **Inbox**: process any files in `docs/inbox/`, extract what belongs in the docs, then
  ask whether to archive or delete each processed file.

For each proposed change: per `brain.config.json`, either propose it and wait for
approval (interactive session) or apply and commit/PR per `writeMode` (headless
session, e.g. the scheduled routine). Summarise proposed changes across all sources in
one message before editing anything; proceed silently if nothing is new.

- **Dashboard**: once the docs above are updated, invoke the `dashboard` skill
  (`skills/dashboard/SKILL.md`) and regenerate `dashboard.status.yaml` wholesale — it
  is never patched. `dashboard.yaml` is human-owned and read-only to an agent: read it
  for ground truth, never write to it.

When the sync is done and anything changed, apply §5's rule on offering to update the
shared copy. A finished sync that leaves the shared copy untouched, without saying so, is
not finished.

## 5. Write-back rules

- Read the canonical source before generating an artefact for it.
- Read existing examples in the target system and match its house style.
- Cite specific anchors in anything you write back.
- Propose before persisting.
- When modifying a live artefact, fetch its current state first and amend that — never
  resend an earlier draft. Humans edit between an AI's writes; a stale draft destroys
  their changes.
- Log every change. After making any edit to this repo, write an entry to `logs/` named
  `YYYY-MM-DD-<short-slug>.md` recording: which agent and command made the change, which
  files changed, which live sources grounded it, what you assumed where a source was
  ambiguous, and what you knowingly left undone. Get the date by running `date` — never
  from memory. See [[logs/README]] for the format. The entry goes in the same commit as
  the change it describes. This is not a substitute for a commit message: the commit says
  what changed, the log entry says what you believed and where you were unsure.

### Always offer to update the shared copy — in plain language

Whenever you have changed anything in this checkout — a doc edit, a sync, a log entry, a
new file — finish by asking whether to update the shared copy. Ask every time, even for a
one-line change, and even if they said yes earlier in the session.

Most people using a brain are not engineers. Do not say "commit", "push", "stage",
"branch" or "remote". Ask:

> Do you want me to update the GitHub repository as well, with the latest changes?

If yes, commit and push per `brain.config.json`'s `writeMode`, then confirm in the same
register — "Updated: the GitHub repository now has the latest changes." If no, say the
changes are saved on this machine only and the shared copy is unchanged, so they know
exactly where things stand.

Never push without asking, and never treat an earlier yes as standing permission for
later changes.

## 6. Guardrails

- No fabrication: never state inferences as facts in committed docs; cite a source or omit.
- No secrets in chat, memory, or committed files.
- No local filesystem paths in shared docs.
- `docs/inbox/` is transient — never reference its paths from committed docs.
- Explicit approval before commit/push in interactive sessions.
- Re-read live sources for source-sensitive questions; the summaries here are cache, not truth.
- Never pull from Loomery-internal Granola folders or other Slack workspaces.
