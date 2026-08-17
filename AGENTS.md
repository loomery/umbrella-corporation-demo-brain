# Umbrella Corporation — Agent Instructions

## Quick facts

- **Project:** Umbrella Corporation
- **Engagement phase:** TODO(brain): current phase (discovery / delivery / etc.)
- **Key contacts:** TODO(brain): client-side and Loomery-side stakeholders (see `docs/stakeholders.md`)

## Before you do anything

Before answering any question about Umbrella Corporation, read `skills/brain/PLAYBOOK.md` and
follow it — it is the map of this repo and its live sources. Never answer project
questions from memory alone.

## Repo layout

```
umbrella-corporation-brain/
├── AGENTS.md
├── CLAUDE.md
├── README.md
├── brain.config.json
├── sources.yaml
├── skills/                # skills live here, one folder each: skills/<name>/SKILL.md.
│   ├── brain/{SKILL.md,PLAYBOOK.md}   # the playbook is a resource of the skill, so it
│   │                      # travels wherever the skill does — including chat
│   └── onboard/{SKILL.md,ONBOARDING.md}
│                          # .claude/skills and .agents/skills are symlinks to this
│                          # directory, so a skill added here works in every tool.
├── docs/
│   ├── engagement.md
│   ├── stakeholders.md
│   ├── meetings.md
│   ├── product-context.md
│   ├── inbox/            # transient — never reference its paths from committed docs
│   ├── source-materials/
│   └── technical/
│       ├── context.md
│       ├── stack.md
│       └── decisions.md
├── logs/                  # one file per change session — what each agent did and assumed
└── src/                   # client code as git submodules — see src/README.md
```

## Hard rules

- No fabrication: never state inferences as facts in committed docs; cite a source or omit.
- No secrets in chat, memory, or committed files (transcripts persist on disk).
- No local filesystem paths in shared docs.
- Cross-link docs: when writing or updating a doc, add wikilinks (e.g. `[[docs/stakeholders]]`) to other relevant docs — a doc left unlinked from the rest of the brain is incomplete.
- `docs/inbox/` is transient — never reference its paths from committed docs.
- Explicit approval before commit/push in interactive sessions.
- Re-read live sources for source-sensitive questions; the summaries here are cache, not truth.
- Individual privacy: only pull from the shared folders/channels named in `sources.yaml`; never from private messages or other clients' spaces.
- Log every change to `logs/` — see `skills/brain/PLAYBOOK.md` §5. A change with no log entry is incomplete.
