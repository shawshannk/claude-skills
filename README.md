# claude-skills

A Claude Code plugin marketplace with skills I use day to day. Each skill is its own
plugin, so you can install only the ones you want.

## Install

In Claude Code:

```
/plugin marketplace add shawshannk/claude-skills
/plugin install project-tech-learning@shawshannk
/plugin install modular-project-builder@shawshannk
```

Then restart Claude Code (or run `/plugin` to confirm they're enabled).

## Plugins

### project-tech-learning

Learn a technology from how it is *actually used* in the current codebase — not a
generic tutorial. Traces execution flow through real files, covers safe modification,
realistic debugging, and what you can honestly claim on a resume.

Invoke with `/project-tech-learning <technology>`, or just ask Claude to explain how a
framework, library, or datastore is used in the repo you're in.

### modular-project-builder

Interview-driven project builder. Turns an idea into a persistent spec (`SPEC.md`), a
modular implementation plan (`PLAN.md`), and progress tracking (`PROGRESS.md`), then
implements one module per session so you never run out of context mid-build.

Invoke with `/modular-project-builder`, or say "let's build X", "new project", or
"continue where we left off".

## Manual install (no plugin system)

```
git clone https://github.com/shawshannk/claude-skills.git
cp -r claude-skills/plugins/*/skills/* ~/.claude/skills/
```

## Updating

```
/plugin marketplace update shawshannk
```

## Adding a skill to this repo

1. `plugins/<name>/.claude-plugin/plugin.json` — name, version, description, author
2. `plugins/<name>/skills/<name>/SKILL.md` — the skill itself (plus any `references/`,
   `scripts/`, or other files it loads)
3. Append an entry to the `plugins` array in `.claude-plugin/marketplace.json`
