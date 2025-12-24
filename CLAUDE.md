# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Claude Code plugin providing Chart.js v4.5.1 expertise. The plugin includes skills (knowledge), commands (user-invocable actions), and an agent (autonomous helper) organized in a marketplace structure.

## Repository Structure

```
plugins/
├── .claude-plugin/plugin.json    # Plugin manifest
├── agents/chartjs-expert.md      # Proactive agent for Chart.js work
├── commands/component.md         # /chartjs:component command
└── skills/                       # 10 specialized knowledge skills
    ├── chartjs-overview/         # Installation, setup, instance methods
    ├── chartjs-chart-types/      # Line, bar, pie, radar, etc.
    ├── chartjs-configuration/    # Options, legends, tooltips, responsiveness
    ├── chartjs-axes/             # Scales, time series, styling
    ├── chartjs-plugins/          # Custom plugin development
    ├── chartjs-developers/       # Custom charts, scales, API
    ├── chartjs-integrations/     # React, Vue, Angular, Rails 8
    ├── chartjs-animations/       # Animation configuration
    ├── chartjs-tooltips/         # Tooltip customization
    └── chartjs-advanced/         # Gradients, advanced techniques
```

`.claude-plugin/marketplace.json` defines the marketplace that hosts this plugin.

## Linting Commands

```bash
# Markdown (plugin content)
markdownlint '**/*.md'

# HTML (example files)
npx htmlhint 'plugins/**/examples/*.html'

# YAML (workflows, config)
yamllint -c .yamllint.yml .github/ .claude-plugin/ plugins/*/.claude-plugin/

# Broken links (markdown files)
lychee --cache '**/*.md'
```

## Plugin Component Rules

When editing plugin components, follow these conventions:

### Skills (`skills/*/SKILL.md`)

- YAML frontmatter requires `name` and `description`
- `description` must start with "This skill should be used when..." and include trigger phrases
- Body contains core knowledge, not exhaustive docs

### Commands (`commands/*.md`)

- YAML frontmatter requires `name`, `description`, `allowed-tools`
- `description` must be 60 characters or fewer
- Use imperative voice in body ("Do X" not "You should X")
- `allowed-tools` should be minimal and appropriate for the command's purpose

### Agents (`agents/*.md`)

- YAML frontmatter requires `name`, `description`, `model`, `color`, `tools`
- `description` must include 2-4 `<example>` blocks with Context, user/assistant dialogue, and `<commentary>`
- `model: inherit` uses the parent model

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
