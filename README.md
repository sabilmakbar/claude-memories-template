# claude-memories-template

Template for a private Claude Code memory repo, ready to pair with
[claude-memory-kit](https://github.com/sabilmakbar/claude-memory-kit). The kit provides
the machinery (index engine, hooks, commit guardrail, feedback miner, review skills);
this repo holds just your data — memory files and, optionally, your global guidelines.

## What's in here

| File | What it is |
|------|-----------|
| `user_example.md` | Who you are — role, background, working style. Rename and fill in. |
| `feedback_example.md` | One working-preference rule in the What/Why/How format. Copy the shape for every new rule. |
| `AGENTS.md` | Optional: global guidelines loaded into every session. Import it from `~/.claude/CLAUDE.md` (see below). |
| `MEMORY.md` | The always-loaded index. Generated from the files on every prompt — never edit by hand. |
| `.gitignore` | Keeps machine-local state and kit-seeded convention files out of sync. |

## Getting started

> Already created your memories repo on another machine? **Don't use the template
> again** — clone your existing repo to `~/.claude/memory` instead (see the kit README's
> "Every other machine" section). One repo, every machine.

1. Click **Use this template** → create your own **private** repo (it will hold personal data).
2. On your machine:

```bash
git clone https://github.com/sabilmakbar/claude-memory-kit.git ~/claude-memory-kit
git clone <your-new-repo> ~/.claude/memory
~/claude-memory-kit/install.sh
printf '@~/.claude/memory/AGENTS.md\n' > ~/.claude/CLAUDE.md   # optional: global guidelines
```

The kit's installer deploys its hooks and skills, seeds the memory-authoring conventions,
and wires this repo's commit guardrail automatically. Start a new Claude Code session and
you're done.

3. Rename the example files to yours (`user_<you>.md`), rewrite their contents, and
   commit. The guardrail checks every commit for naming/frontmatter conventions and
   private-data leaks (emails, home paths — add employer terms to the kit's
   `denylist.local`).

## Conventions (enforced by the guardrail)

- Filename prefix `user_` / `feedback_` / `project_`; `name:` in frontmatter equals the
  filename slug; one-line `description:` required.
- Body = the rule itself, then `**Why:**` and `**How to apply:**`. Generalized — no
  incident stories, no employer names, no machine paths.
- `MEMORY.md` is tracked but the installer marks it `skip-worktree` locally, so index
  churn never shows up in your diffs.

## Review markers (multi-machine)

Periodic memory reviews are recorded as ordinary commits whose subject starts
`memory review (<machine-label>): …` — the kit's review skill writes them (an empty
commit when nothing changed). The session-start reminder reads these markers straight
from git history: a review on **any** machine silences the reminder everywhere once
pushed/pulled, while each machine's own mount-local memories still want a marker from
that machine's label. No state files to manage — history is the single source of truth.
