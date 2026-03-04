# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a Claude Code plugin marketplace containing AI-powered productivity tools, product management workflows, and development automation. Plugins are installed via `/plugin install <name>@jkramer-marketplace`.

## Architecture

### Marketplace Registry
`.claude-plugin/marketplace.json` - Central registry defining all available plugins and standalone skills. Each entry has `source` pointing to plugin location.

### Plugin Structure
Each plugin in `plugins/` follows this convention:
```
plugins/<name>/
├── .claude-plugin/plugin.json    # Metadata (name, version, keywords)
├── commands/                     # Slash commands (*.md files)
├── skills/                       # Skills with SKILL.md + references/
├── agents/                       # Autonomous agents (*.md)
└── hooks/hooks.json             # Event hooks (optional)
```

### Standalone Skills
`skills/` contains skills not bundled with plugins. Same structure as plugin skills:
```
skills/<name>/
├── SKILL.md                     # Main skill definition
└── references/                  # Supporting templates and guides
```

## Key Plugins

| Plugin | Purpose | Key Files |
|--------|---------|-----------|
| `product-management` | WINNING filter, gap analysis, GitHub Issues integration | `skills/product-management/SKILL.md`, `agents/*.md` |
| `mvp-launch` | 10-point launch readiness checker | `skills/mvp-launch/SKILL.md` |
| `deckling` | PPTX generation via Anthropic Platform Skills | `scripts/deckling_worker.py` |
| `jkramer` | Meeting notes → Notion, Excalidraw diagrams | `skills/meeting-notes/`, `skills/excalidraw/` |
| `product-manager-prompts` | PM frameworks (JTBD, positioning, user stories) | 8 skills in `skills/` |

## Deckling Worker

`plugins/deckling/scripts/deckling_worker.py` - Python script calling Anthropic Platform Skills API.

```bash
# Generate new presentation
python3 deckling_worker.py "Topic"

# Refine existing
python3 deckling_worker.py "Make title blue" --refine deck.pptx

# Recover by file ID
python3 deckling_worker.py "file_id" --recover
```

Requires `ANTHROPIC_API_KEY` environment variable. Uses agentic loop with `skills-2025-10-02` beta.

## Product Management Data

The product-management plugin stores data in `.pm/` at project root:
- `config.md` - Positioning, scoring weights
- `competitors/` - Competitor profiles
- `gaps/` - Gap analyses with WINNING scores
- `requests/` - Synced GitHub Issues
- `prds/` - Generated PRDs

## Adding New Plugins

1. Create `plugins/<name>/.claude-plugin/plugin.json` with metadata
2. Add commands in `commands/` and/or skills in `skills/`
3. Register in `.claude-plugin/marketplace.json` under `plugins` array
4. For skills with agents, add agent definitions in `agents/`

## Adding New Skills

Skills use YAML frontmatter in SKILL.md:
```yaml
---
name: skill-name
description: Trigger description for Claude to match
version: 1.0.0
---
```

Reference files go in `references/` subdirectory and are loaded on-demand.
