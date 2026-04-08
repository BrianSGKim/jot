---
description: Quick-capture ideas to scoped scratchpads (work or personal) with optional git sync
user-invocable: true
argument: "<flags> <idea text>" — see --help for usage
---

# /jot — Quick Idea Capture

A shareable Claude Code skill for capturing ideas into scoped scratchpads with optional git backup.

## Language

Read `~/.claude/jot-config.json` and check the `lang` field. All user-facing output (confirmations, help text, error messages, prompts, and "Why it matters" notes) MUST be in that language. If no config exists or lang is missing, default to English.

| lang | Language |
|------|----------|
| `en` | English |
| `ko` | Korean |
| `ja` | Japanese |

The idea text itself is never translated — store it exactly as the user typed it.

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
| `--lang <en\|ko\|ja>` | Change display language |

If no recognized flag is found, respond with the `--help` output.

---

## --help

Print usage instructions in the configured language and stop.

English version:
```
/jot — Quick idea capture to scoped scratchpads

Usage:
  /jot --work <idea>              Save an idea to your work scratchpad
  /jot --me <idea>                Save an idea to your personal scratchpad
  /jot --list work                Show recent work ideas
  /jot --list me                  Show recent personal ideas
  /jot --setup                    First-time setup (configure paths & repos)
  /jot --work --newrepo <url>     Change work git repo
  /jot --me --newrepo <url>       Change personal git repo
  /jot --lang <en|ko|ja>          Change display language

Config: ~/.claude/jot-config.json
```

For ko/ja: translate the descriptions but keep flag names and paths as-is.

---

## --setup

Walk the user through first-time configuration. All prompts in the configured language (or ask language first if no config exists).

1. Ask: "Preferred language? (en/ko/ja)"
2. For each scope (work, me):
   - Ask: "Where should [scope] ideas be stored?" (a directory path — ideas.md will be created here)
   - Ask: "Git repo URL for [scope]? (leave blank for no git sync)"

Write the config to `~/.claude/jot-config.json`:
```json
{
  "lang": "en",
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

1. **Read config** from `~/.claude/jot-config.json`. If it doesn't exist, tell the user to run `/jot --setup` first (in English as fallback).

2. **Read the ideas file** for the chosen scope.

3. **Detect the project context** from the current working directory. The project tag is the root folder name of the current project (e.g., if CWD is `C:\Users\USER\Documents\Sazo\work_updates`, the tag is `work_updates`). This is informational context, not a required field — it helps trace where the idea came from if needed later.

4. **Append** the new entry:
   ```

   ### <short title> (<YYYY-MM-DD HH:MM>) `#project-name`
   <the idea exactly as typed by the user>
   > Why it matters: <one-line contextual note in the configured language>
   ```

   - **Date and time:** Use the current local date and 24h time (`YYYY-MM-DD HH:MM`)
   - **Project tag:** Append `` `#<project-folder-name>` `` after the timestamp. Use the root folder name of the current working directory. If no project context is available, omit the tag.

5. **Confirm** with one line in the configured language. User is in flow.

---

## --list

Read the ideas file for the specified scope. Print the last ~10 `### ` headings with their first line of content. Keep it scannable.

---

## --newrepo

1. Parse: which scope (`--me` or `--work`) and the URL.
2. Read `~/.claude/jot-config.json`.
3. Update the `repo` field for that scope.
4. Write the config back.
5. Confirm in configured language.

---

## --lang

1. Parse the language code (en, ko, ja).
2. Read `~/.claude/jot-config.json`.
3. Update the `lang` field.
4. Write the config back.
5. Confirm in the NEW language.

---

## Notes for anyone adapting this skill

- All files are user-scoped — nothing is written to project directories or project-scoped memory
- Config lives at `~/.claude/jot-config.json` — edit it directly if you prefer
- Ideas files are plain markdown, portable, and grep-friendly
- Git sync is manual (push when you want to back up) — this skill doesn't auto-push
- To use: copy `jot.md` to `~/.claude/commands/` and run `/jot --setup`
- Supports English, Korean, and Japanese — set during setup or change with `--lang`
