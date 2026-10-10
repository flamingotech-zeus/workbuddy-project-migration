# Workspace Project Migration

[English](README.md) | [简体中文](README.zh-CN.md)

> Move scripts, intermediate data and notes out of scattered temporary workspaces into a proper project, rewriting stale absolute paths so everything still runs.

## What this is

This is not a folder-move. Moving files is trivial; the thing that breaks afterwards is every hard-coded path inside the scripts.

The skill treats the move and the path rewrite as one operation, which is the only way the result is usable rather than merely tidy.

## Why we open-sourced it

Temporary working directories accumulate: a few scripts, some JSON output, a notes file. At some point one of them turns out to be worth keeping, and it is sitting in a folder named after a date.

We do this whenever a throwaway workflow earns promotion to a real project. It is packaging logic with nothing proprietary in it.

## What it does

- **Two questions asked up front.** Where should the project live, and what happens to the originals — copied and kept, moved so only one copy exists, or indexed in place. Guessing here produces a mess that is worse than the original.
- **Path rewriting as a first-class step.** Scripts are scanned for absolute paths and rewritten to the new location, so they run from the new home without hand-editing.
- **A root index document** describing what each piece is, so the project is navigable without opening every file.
- **Reversibility.** The operation is documented well enough that a rollback is possible.

## Requirements

Python 3 (or done by hand)

## Installation

```bash
git clone https://github.com/<your-username>/workbuddy-project-migration.git
```

Then place the folder into your agent skills directory:

| OS | Path |
|---|---|
| Windows | `C:\Users\<you>\.workbuddy\skills\workbuddy-project-migration\` |
| macOS / Linux | `~/.workbuddy/skills/workbuddy-project-migration/` |

There is no build step. Restart the session and it takes effect.

## How to use

Ask for the consolidation:

- "Move these into a proper project"
- "Keep only one copy, make it a real project"
- "Fix the paths so the scripts still run"

The skill asks the two scoping questions first, then moves and rewrites in one pass.

## Files

```
└── SKILL.md
```

## Notes and limits

1. **Path rewriting is pattern-based.** Paths assembled dynamically at runtime may not be caught. After migrating, run the scripts once to confirm.
2. **Moving without a copy is irreversible.** That option is offered because it avoids duplicate sources of truth, but choose it knowingly.
3. **Temporary files should not migrate.** Intermediate output usually should not follow the scripts into the new project; the index documents where it came from instead.
4. **Git history does not travel.** If the original folder was a repository, the move does not carry that history across unless done deliberately.

## License

MIT
