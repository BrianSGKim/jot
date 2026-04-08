---
description: Quick-capture ideas to scoped scratchpads (work or personal) with optional git sync
user-invocable: true
argument: "<flags> <idea text>" — see --help for usage
---

# /jot — Quick Idea Capture

A shareable Claude Code skill for capturing ideas into scoped scratchpads with optional git backup.

## Parsing

Parse `$ARGUMENTS` for flags and idea text:

**Raw input:** $ARGUMENTS

### Flags

| Flag | Purpose |
|------|---------|
| `--help` | Show usage instructions. Do nothing else. |
| `--me <idea>` | Append idea to personal scratchpad |
| `--work <idea>` | Append idea to work scratchpad |
| `--list` | Show last ~10 ideas from a scope. Usage: `--list me` or `--list work` |
| `--setup` | First-time configuration wizard |
| `--newrepo <url>` | Change the git repo for a scope. Usage: `--me --newrepo <url>` or `--work --newrepo <url>` |

If no recognized flag is found, respond with the `--help` output.

---

## --help

Print this and stop:

```
/jot — Quick idea capture to scoped scratchpads

Usage:
  /jot --work <idea>        Save an idea to your work scratchpad
  /jot --me <idea>          Save an idea to your personal scratchpad
  /jot --list work          Show recent work ideas
  /jot --list me            Show recent personal ideas
  /jot --setup              First-time setup (configure paths & repos)
  /jot --work --newrepo <url>   Change work git repo
  /jot --me --newrepo <url>     Change personal git repo

Config: ~/.claude/jot-config.json
```

---

## --setup

Walk the user through first-time configuration. For each scope (work, me):

1. Ask: "Where should [scope] ideas be stored?" (a directory path — the ideas.md file will be created here)
2. Ask: "Git repo URL for [scope]? (leave blank for no git sync)"

Write the config to `~/.claude/jot-config.json`:
```json
{
  "work": {
    "ideas_file": "<path>/ideas.md",
    "repo": "<url or null>"
  },
  "me": {
    "ideas_file": "<path>/ideas.md",
    "repo": "<url or null>"
  }
}
```

Create `ideas.md` in each directory if it doesn't exist:
```markdown
# Ideas

Running scratchpad of ideas, tidbits, and observations.
```

---

## --me / --work (core capture)

1. **Read config** from `~/.claude/jot-config.json`. If it doesn't exist, tell the user to run `/jot --setup` first.

2. **Read the ideas file** for the chosen scope.

3. **Append** the new entry:
   ```

   ### <short title> (<YYYY-MM-DD>)
   <the idea as stated>
   > Why it matters: <one-line contextual note if obvious from the idea or conversation>
   ```

4. **Confirm** with one line. User is in flow.

---

## --list

Read the ideas file for the specified scope. Print the last ~10 `### ` headings with their first line of content. Keep it scannable.

---

## --newrepo

1. Parse: which scope (`--me` or `--work`) and the URL.
2. Read `~/.claude/jot-config.json`.
3. Update the `repo` field for that scope.
4. Write the config back.
5. Confirm: "Updated [scope] repo to <url>"

---

## Notes for anyone adapting this skill

- All files are user-scoped — nothing is written to project directories or project-scoped memory
- Config lives at `~/.claude/jot-config.json` — edit it directly if you prefer
- Ideas files are plain markdown, portable, and grep-friendly
- Git sync is manual (push when you want to back up) — this skill doesn't auto-push
- To use: copy `jot.md` to `~/.claude/commands/` and run `/jot --setup`
