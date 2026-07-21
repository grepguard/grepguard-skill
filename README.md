# GrepGuard skill

Use this skill to run AI agent work in GrepGuard cloud sandboxes. It guides the agent through setup, running a task, and checking logs.

Installing the skill does not install GrepGuard. The agent will help you install and sign in to the `grepguard` CLI when needed.

## Install

Run these commands from this folder.

### Codex

```bash
mkdir -p ~/.codex/skills/grepguard-skill
cp SKILL.md ~/.codex/skills/grepguard-skill/
```

### OpenCode

Install globally to use the skill in every project:

```bash
mkdir -p ~/.config/opencode/skills/grepguard-skill
cp SKILL.md ~/.config/opencode/skills/grepguard-skill/
```

Or install it only in the current project:

```bash
mkdir -p .opencode/skills/grepguard-skill
cp SKILL.md .opencode/skills/grepguard-skill/
```

Start a new Codex or OpenCode session after installing.

## Use it

Ask your agent to use GrepGuard. For example:

```text
Create a simple namespace and pod with OpenCode, then run a hello task.
```
