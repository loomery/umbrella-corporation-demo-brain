# src/

Client code lands here as git submodules, one per repository:

```bash
git submodule add <url> src/<RepoName>
```

Before opening any submodule, check `docs/technical/stack.md` — it maps each submodule
to what it is and how it fits together.

On a fresh clone: `git submodule update --init` pulls the submodule contents (they are
not fetched by a plain `git clone`).

Submodule access is per-user on the client's GitHub org — if a submodule won't clone,
confirm your account has been added to the client's org before assuming the URL or
config is wrong.
