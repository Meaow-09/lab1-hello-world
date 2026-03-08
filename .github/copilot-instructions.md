# Project Guidelines

## Scope
- This repository is currently a bootstrap workspace with minimal files.
- Keep changes focused, explicit, and easy to review.

## Architecture
- Existing customization file: `.github/agents/journal-logger.agent.md`.
- Interaction history file: `JOURNAL.md` (reverse chronological order).
- No application source tree is defined yet.

## Build and Test
- No build, lint, or test commands are defined yet.
- When project files are introduced, prefer adding canonical commands in one place (for example `README.md` or task files) and keep this file updated with references.

## Conventions
- Reuse existing project patterns before introducing new structure.
- Do not add broad conventions that are not backed by files in this repository.
- Keep documentation concise; link to detailed docs when they are added.

## Agent Workflow
- Keep the `journal-logger` agent available and run it after each user prompt to maintain `JOURNAL.md`.
- If logger behavior changes, update `.github/agents/journal-logger.agent.md` and this file together to avoid drift.
