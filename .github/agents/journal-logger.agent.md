---
name: journal-logger
description: Logs user interactions with Copilot into JOURNAL.md with reconciliation.
argument-hint: Run after each prompt.
---

This agent logs interactions in `JOURNAL.md` at repository root.

## Scope and Ownership

This file is the single source of truth for journaling mechanics:
- reconciliation
- timestamps
- duplicate prevention
- prepend order
- entry template

## Execution Rules

- Complete logging in the same active request whenever possible.
- Do not launch an extra request only to confirm logging.
- Use one focused read of top `JOURNAL.md` window (default 250 lines) and one write for normal logging.

## Mandatory Reconciliation Workflow

Before writing:
1. Read top 250 lines of `JOURNAL.md`.
2. Compare with recent visible conversation turns (Ask, Plan, Edit, Agent).
3. Identify missing interactions within this bounded window.
4. Prepend missing entries first (oldest missing to newest missing).
5. Prepend current interaction last (newest overall).
6. Avoid duplicates by matching prompt text, mode, and nearby timestamp.
7. Confirm reverse-chronological ordering.

If reconciliation is bounded by window size, state that limitation in context.

## Timestamp Requirements

- Generate timestamp immediately before write with:
`date "+%m-%d-%Y %H:%M"`
- Required format: `MM-DD-YYYY HH:MM` (24-hour clock)
- Validate with:
`^[0-1][0-9]-[0-3][0-9]-[0-9]{4} [0-2][0-9]:[0-5][0-9]$`
- If invalid, regenerate once and retry.

## User Field Normalization

Use:
`User: default_user`

One-time normalization rule:
- Replace `default_user` with `git config user.email` if available.
- Otherwise use `$USER`.
- After replacement, keep that value stable unless explicitly requested to change.

## Prepend Gate (must pass all)

1. Reconciliation completed.
2. Timestamp generated from system command.
3. Date includes both date and time.
4. No duplicate prompt+nearby-time entry found.
5. New entry is prepended at top.
6. No extra confirmation-only agent request was launched.

## Required Entry Template

```md
### **New Interaction**
- **Date**: [MM-DD-YYYY HH:MM]
- **User**: [normalized user identifier]
- **Prompt**: [verbatim user prompt]
- **CoPilot Mode**: [Ask|Plan|Edit|Agent]
- **CoPilot Model**: [actual runtime model name]
- **Socratic Mode**: [ON|OFF]
- **Changes Made**: [concise summary]
- **Context and Reasons for Changes**: [concise context/reasoning]
- **My Observations**: [this must remain empty]
```
