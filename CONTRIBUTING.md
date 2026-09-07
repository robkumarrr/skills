# Contributing & Editing Guide

Welcome back! This document serves as a reminder for how to maintain and add new skills to this repository.

## The Branching Strategy

Because branch protection is enabled on `main`, you cannot push directly to it.
Instead of maintaining a persistent `dev` branch, use the **GitHub Flow**:

1. Check out a new branch: `git checkout -b feat/my-new-skill`
2. Make your edits or add a new skill.
3. Push the branch and open a Pull Request against `main`.
4. Wait for the `markdownlint` CI to pass.
5. Merge into `main`!

## Anatomy of an S-Tier Skill

When adding a new skill, ensure it follows the strict format that AI agents expect.

### 1. The Frontmatter

Every `SKILL.md` MUST start with a YAML frontmatter block. The description is critical—it is the only thing the agent reads to decide if it should activate the skill. Keep it precise.

```yaml
---
name: my-skill-name
description: "Exactly when the agent should use this skill. Be specific."
---
```

### 2. Be Mechanical, Not Theoretical

Agents do not need theory. Give them exact, executable commands.

- **Bad:** "Make sure the code runs."
- **Good:** "Run `npm run test` and verify all suites pass."

### 3. Be Defensive (Anti-patterns)

Agents are lazy and love shortcuts. Always include an **Anti-patterns** section that explicitly bans the shortcuts you know the AI will try to take.

- e.g., "Do not use `git add .`" or "Do not mock internal collaborators."

## Formatting Reminders

This repository uses a strict Markdown linter in CI. We have intentionally disabled the 80-character line limit, but `markdownlint` is still strict about trailing spaces and blank lines.

Before pushing your branch, you can automatically fix all formatting errors by running:

```bash
npx markdownlint-cli2 "**/*.md" --fix
```

Alternatively, installing the `markdownlint` editor extension (by David Anson) will highlight and auto-fix these for you on save!
