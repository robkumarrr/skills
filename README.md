# Robert's Agent Skills

A collection of high-quality, specialized skills for AI coding agents (compatible with `skills.sh`, Claude Code, Cursor, Antigravity, etc.).

These skills are designed to enforce strict engineering discipline and prevent agents from taking lazy shortcuts.

## 🚀 Installation

To teach your AI agent these skills, navigate to your project directory and run:

```bash
npx skills@latest add robertkumar/skills
```

*(This interactive CLI will let you select which specific skills from this repository you want to install into your project).*

## 🛠️ Available Skills

### `atomic-commits`

Enforces atomic commits and disciplined version control for AI agents.

- **Prevents "Kitchen Sink" commits:** Explicitly bans the agent from using `git commit -am` or `git add .` when dealing with mixed changes.
- **Forces Surgical Staging:** Requires the agent to use `git add -p` and verify changes with `git diff --cached`.
- **Enforces Conventional Commits:** Enforces standard `<type>: <description>` formatting.

---

*See [CONTRIBUTING.md](./CONTRIBUTING.md) for notes on how to add and format new skills.*
