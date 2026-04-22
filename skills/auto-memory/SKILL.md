---
name: auto-memory
description: Use when starting or ending work in a project where project context, task goals, decisions, tools, or session state should survive a new chat, reopened agent, or context switch
---

# Auto Memory

## Overview

Keep a durable project memory at `.agent/memory.md` in the current project root. The memory must let a future agent reopen the folder and understand the project state, task goals, important decisions, commands, tools, and next steps without relying on chat history.

## When to Use

- At the start of work in a project, especially after opening a new session.
- Before switching chats, closing the agent, compacting context, or pausing work.
- After meaningful changes to goals, files, commands, blockers, decisions, or verification status.

Do not use for secrets, credentials, private keys, or long raw logs.

## Core Rule

Always target the project-local path:

```text
<project-root>/.agent/memory.md
```

If `.agent/memory.md` is missing, inspect the project folder and create a current-state memory.

If `.agent/memory.md` exists, read it first, then compress and update it with the current session context. Preserve durable facts, remove stale detail, and keep the file useful for reopening the project later.

## Workflow

1. Confirm the project root with `pwd`.
2. Check whether `.agent/memory.md` exists.
3. If missing, inspect the folder with fast read-only commands such as `find`, `rg --files`, `ls`, and selected file reads.
4. If present, read `.agent/memory.md` before editing.
5. Write a compact memory that includes the current project state and session context.
6. Keep the memory comprehensive enough to resume work, but avoid dumping raw command output.

## Memory Format

```markdown
# Project Memory

## Snapshot
- Date:
- Project root:
- Current status:

## Project State
- Key files and folders:
- Generated artifacts:
- Missing or empty areas:

## Task Goals
- Active goal:
- User preferences or constraints:

## Decisions
- Important choices made:
- Paths or tools selected:

## Commands and Verification
- Commands run:
- Verification status:

## Next Steps
- Immediate next action:
- Known blockers:
```

## Quick Reference

| Situation | Action |
| --- | --- |
| No `.agent/memory.md` | Inspect project, create current-state memory |
| Existing `.agent/memory.md` | Read, compress, update, preserve durable facts |
| Long terminal output | Summarize the result and keep key commands |
| Sensitive data appears | Do not write it to memory |
| Unsure where to write | Use the current project root, not the home directory |

## Common Mistakes

- Writing to `~/.agent/memory.md` instead of project-local `.agent/memory.md`.
- Creating memory from chat alone without inspecting project files.
- Appending endlessly instead of compressing stale context.
- Omitting task goals, key tools, verification status, or blockers.
- Saving secrets or raw logs that future agents do not need.

