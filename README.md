# MyAI Marketplace

A personal plugin marketplace for Claude Code with AI automation skills, plugins, and commands.

## Installation

Add this marketplace to Claude Code:

```bash
/plugin marketplace add /path/to/MyAI
```

Then install any plugin:

```bash
/plugin install deckling@jkramer-marketplace
/plugin install product-management@jkramer-marketplace
```

## Plugins

| Name | Commands | Description |
|------|----------|-------------|
| [deckling](./plugins/deckling) | `/deckling` | Generate PPTX presentations using Anthropic Platform Skills API |
| [mvp-launch](./plugins/mvp-launch) | `/launch-check` | MVP launch readiness checker with 10-point checklist |
| [product-management](./plugins/product-management) | `/pm:*` | AI-native PM: competitive research, gap analysis, WINNING prioritization |

## Skills

| Name | Triggers | Description |
|------|----------|-------------|
| [meeting-notes](./skills/meeting-notes) | "meeting notes", "process this meeting" | Process transcripts into Notion summaries + action items |
| [excalidraw](./skills/excalidraw) | "architecture diagram", "excalidraw" | Generate `.excalidraw` diagrams from codebase analysis |
| [uat-testing](./skills/uat-testing) | "run UAT", "test this feature" | End-to-end acceptance testing with Playwright |

## Quick Reference

### Product Management (`/pm:*`)
```
/pm:analyze     # Understand current product
/pm:landscape   # Research competitors
/pm:gaps        # Identify & score gaps (WINNING filter)
/pm:file        # Create GitHub Issues
/pm:prd         # Generate full PRD
/pm:sync        # Sync with GitHub
```

### Deckling
```
/deckling "Quarterly Review - 3 slides"
/deckling "Make title blue" --refine deck.pptx
```

### MVP Launch
```
/launch-check   # Run 10-point readiness audit
```

## Credits

The following skills and plugins are adapted from [ooiyeefei/ccc](https://github.com/ooiyeefei/ccc):
- deckling
- mvp-launch
- product-management
- excalidraw
