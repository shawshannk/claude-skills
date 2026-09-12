# claude-skills

A Claude Code plugin marketplace with skills I use day to day.

## Install

In Claude Code:

```
/plugin marketplace add shawshannk/claude-skills
/plugin install project-tech-learning@shawshannk
```

Then restart Claude Code (or run `/plugin` to confirm it's enabled).

## Plugins

### project-tech-learning

Learn a technology from how it is *actually used* in the current codebase — not a
generic tutorial. Traces execution flow through real files, covers safe modification,
realistic debugging, and what you can honestly claim on a resume.

Invoke it with `/project-tech-learning <technology>`, or just ask Claude to explain
how a framework/library/datastore is used in the repo you're in.

## Manual install (no plugin system)

```
git clone https://github.com/shawshannk/claude-skills.git
cp -r claude-skills/plugins/project-tech-learning/skills/project-tech-learning ~/.claude/skills/
```

## Updating

```
/plugin marketplace update shawshannk
```
