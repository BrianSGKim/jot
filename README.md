# /jot

A [Claude Code](https://claude.ai/claude-code) skill for quick-capturing ideas into scoped scratchpads.

Keep a running log of ideas, tidbits, and observations — separated by scope (work vs personal) — with optional git backup.

## Install

```bash
# One-liner
curl -o ~/.claude/commands/jot.md https://raw.githubusercontent.com/BrianSGKim/jot/main/jot.md
```

Or manually: copy `jot.md` to `~/.claude/commands/`.

## Setup

Run once after installing:

```
/jot --setup
```

This walks you through configuring paths for your work and personal scratchpads, plus optional git repo URLs for backup.

Config is stored at `~/.claude/jot-config.json`.

## Usage

```
/jot --work <idea>              Save a work idea
/jot --me <idea>                Save a personal idea
/jot --list work                Show recent work ideas
/jot --list me                  Show recent personal ideas
/jot --work --newrepo <url>     Change work git repo
/jot --me --newrepo <url>       Change personal git repo
/jot --help                     Show usage
```

## Examples

```
/jot --work batch API calls to reduce rate limiting
/jot --me check out that ceramics studio in Itaewon
/jot --list work
```

## How it works

- Ideas are appended to plain markdown files (`ideas.md`) with timestamps
- Two scopes: `--work` and `--me`, each with its own file and optional git repo
- Everything is user-scoped under `~/.claude/` — nothing touches project directories
- Git sync is manual (push when you want to back up)

## File structure after setup

```
~/.claude/
  commands/jot.md          # the skill
  jot-config.json          # your paths + repo URLs
  jot/work/ideas.md        # work scratchpad
  jot/me/ideas.md          # personal scratchpad
```

## Requirements

- [Claude Code](https://claude.ai/claude-code) CLI, desktop app, or IDE extension

## License

MIT
