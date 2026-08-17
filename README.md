## 👋 What is this?

This repo is a public demo of **Loomery's project-brain tooling** — the AI-powered
orientation layer we build for client engagements. "Umbrella Corporation" is a
**fully fictional placeholder client** (no real company, people, or data — see
[NOTICE.md](NOTICE.md) and [docs/onboarding-status.md](docs/onboarding-status.md) for
the full disclosure), invented so this demo could be shown off without touching
anything real. Browse the live site to see the wiki and dashboard this repo generates:

**🔗 [Live demo site](https://<github-username-or-org>.github.io/<repo-name>/)**
<!-- TODO(tom): fill in the real GitHub Pages URL once this repo has been created on GitHub. -->

---

# Umbrella Corporation — Project Brain

Created: 2026-06-15 (engagement kickoff)

> **Demo brain.** Umbrella Corporation is a fictional client, built to demonstrate
> Loomery's project-brain tooling end-to-end without touching real client material.
> Every doc under `docs/` is invented, in the cited style a real brain would use — see
> `docs/onboarding-status.md` for the full disclosure and what a real onboarding would
> do differently. See [NOTICE.md](NOTICE.md) for a note on the "Umbrella Corporation"
> name and logo — no affiliation with Capcom or *Resident Evil*.

This repo is the orientation and routing layer for AI coding agents working on the
Umbrella Corporation engagement. It does not hold the truth itself — `sources.yaml` points
at the live systems that do (Granola, Slack, Linear, Google Drive, Miro, Figma); this
repo holds distilled context, routing, and the client's source code as git submodules.

## Setup

1. Clone with submodules:
   ```bash
   git clone --recurse-submodules <this-repo-url>
   ```
   Already cloned without `--recurse-submodules`? Run `git submodule update --init`.

2. Install the MCP servers for the sources this project uses:



3. Launch Claude Code:
   ```bash
   claude
   ```
   Starting from a subdirectory is fine — Claude Code loads project skills from
   `.claude/skills/` in the starting directory and every parent up to the repo root.

4. Accept the workspace trust dialog when prompted. The hooks in
   `.claude/settings.json` only take effect once you have.

5. Try it:
   ```
   /brain
   ```
   This is the command you'll use every day — ask it anything about Umbrella Corporation.
   The one exception is a brand-new brain, or one still carrying `TODO(brain)`
   markers: run `/onboard` first. It's a one-time setup step, not something you run
   again once it's done — after that, always come back to `/brain`.

## First run — hand it what you've got before you start

A generated brain is a skeleton, not a finished one. `/onboard` connects the sources
you picked, grounds the docs in them, and hands off to `/brain` once that's done — once,
not every time you open this brain.

**Before you type `/onboard`, gather what you already have and give it over.** Don't
just run the skill and leave it to go searching for context on its own — the more you
hand it up front, the less it has to guess or ask you about one thing at a time:
- Any Slack messages or email threads that explain what this engagement is
- The Slack channel, Linear/Jira project, or Drive folder it should actually read from
- A proposal, SOW, kickoff deck, or meeting notes — paste them in, or drop the file into
  `docs/inbox/`
- Who the key people are, client-side and Loomery-side

It will still ask, one question at a time, for anything you didn't already hand over —
this isn't instead of that conversation, it's what makes the conversation shorter and
the early guesses fewer.

It's resumable: stop partway through — end of day, an MCP hiccup, anything — and the
next run picks up from `docs/onboarding-status.md` rather than starting over. That same
file doubles as a handover note, so a colleague picking this brain up later can see
what's grounded, what was assumed, and what's still missing.

## What happens automatically

Claude Code hooks in `.claude/settings.json` do two things:
- **On session start**: check every source in `sources.yaml` for anything newer than
  what the docs reflect, summarise proposed updates before touching anything, and read
  the two or three most recent `logs/` entries for what the last session did.
- **On each prompt**: a reminder to identify and read the live source that owns the
  answer, per `sources.yaml`, rather than answering from memory.

There's deliberately no hook for saving work — a check for "did the docs change?" would
fire on every single turn until the change was actually committed, which is precisely
the loop that used to interrupt onboarding on every message. Saving is handled in the
instructions instead: `/onboard`'s close-out and `skills/brain/PLAYBOOK.md` §5 both write
a `logs/` entry and offer to commit or open a PR, per `brain.config.json`'s `writeMode`,
as the last step of the work rather than a background check running underneath it.

These are a Claude Code-only enhancement — the playbook itself instructs the same
session-start freshness check, so Codex and opencode sessions degrade gracefully rather
than silently missing this behaviour.

## Adding your own skills

Anything this project does repeatedly — a report you keep writing, a checklist you keep
pasting, a multi-step routine — can become a skill. Make a folder under `skills/` with a
`SKILL.md` in it:

```
skills/
├── brain/SKILL.md        # ships with this repo
└── weekly-report/SKILL.md # yours
```

```markdown
---
name: weekly-report
description: >-
  Write the weekly client update for Umbrella Corporation. Use when asked for the weekly
  report, the Friday update, or a summary of the week's progress.
---

Read `PLAYBOOK.md` (this skill's own directory) for the live sources, then draft the update from this week's
meetings and Linear activity. Cite an anchor for every claim.
```

That's the whole job — the folder name is the command, so this one is `/weekly-report`.
Every tool picks it up with nothing to install, re-run, or configure: `.claude/skills`
and `.agents/skills` are symlinks to this same `skills/` directory (see below), so a
skill added once is a skill every tool can see. Commit it and your colleagues get it too.

The `description` is what decides whether the AI reaches for the skill on its own, so
write it as "use when…" and name the words someone would actually say. If a skill you
just added doesn't appear, restart the session — a running one doesn't always notice a
brand-new skill directory.

## Other agents

This repo is agent-agnostic: `AGENTS.md` carries the canonical instructions,
`skills/brain/PLAYBOOK.md` is the single playbook every adapter points at, and the skills
themselves live in one real, visible, root-level directory — **`skills/`** — not hidden
under a dot-directory and not nested under a `<slug>/skills/` path. That's what you edit.

Each tool reads that same directory from its own conventional location, via a symlink:

| Path | Read by |
|---|---|
| `skills/` | — (the one real directory) |
| `.claude/skills` → `../skills` | Claude Code, opencode |
| `.agents/skills` → `../skills` | Codex CLI, opencode |

Windows note: git needs Developer Mode enabled, or checkouts done from an elevated
prompt, for these symlinks to materialise correctly — otherwise they check out as
small text files containing the link's target path instead of working links.

**Codex CLI** — reads `AGENTS.md` automatically, and picks up the `brain` skill from
`.agents/skills/brain/SKILL.md` with no setup step (no more copying anything to
`~/.codex/prompts/` — that mechanism is deprecated upstream in favour of this
repo-shareable skills format). MCP servers — paste into `~/.codex/config.toml`:
   ```toml
# TODO(brain): no source in this project has a public remote MCP endpoint yet — add one here once you have a server.
   ```

**opencode** — reads `AGENTS.md` automatically; picks up the same `brain` skill with
no setup (it scans both `.claude/skills/` and `.agents/skills/`); the `/brain` command
(`.opencode/commands/brain.md`) and `opencode.json`'s MCP config work with no
additional setup beyond authenticating each server on first use.

## Using this brain from another project

Everything above assumes you're sitting inside this repo. You don't have to be — this
brain is also a plugin, installable once and then usable as `/umbrella-corporation:brain` from any
project, without `cd`-ing back here.

**Claude Code:**
```
/plugin marketplace add <this-repo-url-or-local-path>
/plugin install umbrella-corporation@umbrella-corporation-brain
```
The install name is `umbrella-corporation@umbrella-corporation-brain` — the plugin, then the marketplace it came
from. Those read `.claude-plugin/marketplace.json` and `.claude-plugin/plugin.json`.
Neither carries a `version`, so Claude Code versions the install by git commit SHA
instead — every commit to this repo becomes a distinct version, so a refresh picks up
every commit, instead of freezing at the version you first installed. (That is what makes
updating possible; the installed copy still updates when the marketplace and plugin are
refreshed, not on its own.)

**Codex** — the same brain is a Codex plugin via `.codex-plugin/plugin.json` and the
catalogue at `.agents/plugins/marketplace.json`. Per OpenAI's published Codex plugin
docs, registering this repo as a marketplace looks like:
```
codex plugin marketplace add <this-repo-url-or-local-path>
```
with `owner/repo` shorthand, a git URL, or a local path all accepted, and enabling the
plugin itself then happening in the ChatGPT desktop app rather than from the CLI. Both of
those are taken from those docs rather than tried here, so check `codex plugin --help`
against your own version if the command is rejected. Unlike the Claude manifests,
`.codex-plugin/plugin.json` does pin a `version`, because Codex caches by version number
and has no commit-SHA fallback — so bump it if you change the skills.

**opencode** needs no separate install: `.agents/skills` already symlinks to `skills/`
(see above), and opencode reads that directly whether or not the plugin is installed.

Whichever route gets you here — plain `/brain` inside this repo, or `/umbrella-corporation:brain`
installed as a plugin — the skill's first job is always finding a real, writable
checkout of Umbrella Corporation's brain, not just narrating from wherever its files
happened to load from. Installed as a plugin, the harness copies this whole repo into
a read-only cache first; the skill checks the current directory, then a remembered
checkout, then the conventional `~/Documents/Project Brains/Umbrella Corporation`
location, offering to clone this repo if none of those already exist and this brain
knows its own remote (`brain.config.json`'s `remote`, recorded when the brain was
uploaded to GitHub) — and asking you for a path if it doesn't. Only if all of
that fails does it read the cache directly — and when it does, it says so explicitly
and refuses to write, rather than quietly treating a frozen snapshot as current. Your
edits land in a real checkout, never in the plugin cache.
