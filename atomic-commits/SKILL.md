---
name: atomic-commits
description: "Enforce atomic commits and disciplined version control. Use when committing work, breaking down a large diff, or when the user specifically requests atomic commits."
---

# Atomic Commits

An atomic commit is exactly one logical change. It does one thing, it does it completely, and it leaves the codebase in a working state.

When invoked to commit work, you must enforce this discipline mechanically. Never commit a broken state, and never mix unrelated changes.

## Anti-patterns

- **The Kitchen Sink**: Using `git commit -am` or `git add .` when the working tree contains multiple unrelated logical changes (e.g., a bug fix, a feature, and a formatting change). **Fix:** Use `git add -p` or stage specific files to break them apart.
- **The Mixed Refactor**: Combining a structural change (refactoring) with a behavioral change (a new feature) in the same commit. **Fix:** Revert the feature, commit the refactor, then re-apply the feature in a new commit.
- **The "Oops" Commit**: Committing a broken test or build state, followed by a "fix tests" commit immediately after. This breaks `git bisect`. **Fix:** Squash the fix into the broken commit, or run tests *before* committing.

## The Process

When handling unstaged work or breaking down a diff, follow this exact loop:

### 1. Analyze and Plan

Run `git status` and `git diff`. Identify the distinct logical chunks of work. Mentally list out the commits you will need to make to get the working tree clean.

### 2. Stage Surgically

Do not use `git add .` if there are mixed changes.

- Run `git add -p` (if supported) to stage specific hunks, OR manually stage specific files.
- Run `git diff --cached` to explicitly verify that *only* the lines belonging to this specific logical change are staged. If unrelated lines snuck in, `git restore --staged <file>` them out.

### 3. Verify

Before committing, prove the staged code works.

- Run the relevant unit tests or typechecker for the specific area you are committing.
- If it fails, fix the code and update the staged changes before moving forward.

### 4. Write a Conventional Commit

Draft a commit message following the Conventional Commits specification: `<type>(<optional scope>): <description>`.

- `feat`: A new feature
- `fix`: A bug fix
- `refactor`: A code change that neither fixes a bug nor adds a feature
- `test`: Adding missing tests or correcting existing tests
- `chore`: Changes to the build process or auxiliary tools

**The Body**: The subject line should be clear enough to explain *what* changed. A commit body is **optional** and should only be used if the *why* behind the change is highly complex, non-obvious, or if you are preparing a large PR. Do not write filler text.

### 5. Commit and Repeat

Run `git commit -m "<message>"`. If `git status` shows remaining unstaged work, return to Step 1 and repeat the loop until the working tree is completely clean.
