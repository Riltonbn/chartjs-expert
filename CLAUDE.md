# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Claude Code plugin marketplace providing Chart.js v4.5.1 expertise. The marketplace contains one plugin (`chartjs-expert`) with 10 skills, 1 command, and 1 agent.

## Repository Structure

```
.claude-plugin/
└── marketplace.json              # Marketplace manifest (points to plugins/)

plugins/chartjs-expert/
├── .claude-plugin/plugin.json    # Plugin manifest
├── agents/chartjs-expert.md      # Proactive agent for Chart.js work
├── commands/component.md         # /chartjs:component command
└── skills/                       # 10 specialized knowledge skills
    └── chartjs-*/                # Each skill directory contains:
        ├── SKILL.md              # Core knowledge (required)
        ├── references/           # Deep-dive documentation (optional)
        └── examples/             # Working code examples (optional)
```

Skill domains: overview, chart-types, configuration, axes, plugins, developers, integrations, animations, tooltips, advanced.

## Linting Commands

```bash
# Markdown
markdownlint '**/*.md'

# HTML (example files)
npx htmlhint 'plugins/**/examples/*.html'

# YAML
yamllint -c .yamllint.yml .github/ .claude-plugin/ 'plugins/*/.claude-plugin/'

# Broken links
lychee --cache '**/*.md'

# GitHub Actions
actionlint
```

## Plugin Component Rules

When editing plugin components, follow these conventions:

### Skills (`skills/*/SKILL.md`)

- YAML frontmatter requires `name` and `description`
- `description` must start with "This skill should be used when..." and include trigger phrases
- Body contains core knowledge, not exhaustive documentation
- Use `references/` subdirectory for deep-dive documentation on specific topics
- Use `examples/` subdirectory for working code samples (`.html` or `.md`)

### Commands (`commands/*.md`)

- YAML frontmatter requires `name`, `description`, `allowed-tools`
- Optional: `argument-hint` for showing expected arguments
- `description` must be 60 characters or fewer
- Use imperative voice in body ("Do X" not "You should X")
- `allowed-tools` should be minimal and appropriate for the command's purpose

### Agents (`agents/*.md`)

- YAML frontmatter requires `name`, `description`, `model`, `color`, `tools`
- `description` must include 2-4 `<example>` blocks with Context, user/assistant dialogue, and `<commentary>`
- `model: inherit` uses the parent model
- `tools` is a comma-separated list (e.g., `Read, Write, Edit, Grep, Glob, Bash`)

## CI Workflows

PRs run linting automatically based on changed file types. Key workflows:

- `markdownlint.yml` - Markdown files
- `html-lint.yml` - HTML example files
- `yaml-lint.yml` - YAML config files
- `links.yml` - Broken link checking (weekly + on MD changes)
- `component-validation.yml` - Claude-powered validation of plugin components

## Chart.js Reference

This plugin targets **Chart.js v4.5.1**. When adding examples or updating skills:

- Use tree-shaking patterns for production code (manual component registration)
- `chart.js/auto` is acceptable for prototyping examples only
- Include required components: Controllers, Elements, Scales, Plugins
