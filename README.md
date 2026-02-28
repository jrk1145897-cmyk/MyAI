# MyAI Marketplace

A personal Claude Code plugin marketplace with AI-powered productivity tools, product management workflows, and development automation.

## Repository Structure

```
MyAI/
├── .claude-plugin/          # Marketplace configuration
│   └── marketplace.json     # Plugin registry for Claude Code
├── plugins/                 # Installable Claude Code plugins
│   ├── deckling/           # PPTX generation via Anthropic Platform Skills
│   ├── mvp-launch/         # MVP launch readiness checker
│   ├── product-management/ # AI-native PM workflows
│   └── jkramer/            # Personal productivity (meeting notes, diagrams)
└── skills/                  # Standalone skills (not plugin-bundled)
    └── uat-testing/        # End-to-end acceptance testing with Playwright
```

## Installation

Add this marketplace to Claude Code:

```bash
/plugin marketplace add /path/to/MyAI
```

Then install plugins:

```bash
/plugin install deckling@jkramer-marketplace
/plugin install mvp-launch@jkramer-marketplace
/plugin install product-management@jkramer-marketplace
/plugin install jkramer@jkramer-marketplace
```

---

## Plugins

### deckling

Generate native PPTX presentations using Anthropic's Platform Skills API (server-side rendering).

| Command | Description |
|---------|-------------|
| `/deckling` | Create or refine PowerPoint slides |

```bash
/deckling "Quarterly Review - 3 slides"
/deckling "Make title blue" --refine deck.pptx
```

**Tech:** Python worker script, Anthropic Platform Skills API

---

### mvp-launch

Web app launch readiness checker with a battle-tested 10-point checklist.

| Command | Description |
|---------|-------------|
| `/launch-check` | Run gap analysis against launch criteria |

**Checklist areas:** Stripe integration, mobile responsiveness, onboarding flow, AI stability, transactional emails, logging, user feedback, authentication, custom domain, database backups.

**Philosophy:** Don't overbuild. Identifies what's truly needed for launch vs. nice-to-haves.

---

### product-management

AI-native product management for startups. Transforms Claude into an expert PM.

| Command | Description |
|---------|-------------|
| `/pm:analyze` | Scan codebase and interview for product inventory |
| `/pm:landscape` | Research competitor landscape |
| `/pm:gaps` | Run gap analysis with WINNING filter scoring |
| `/pm:file` | Batch create GitHub Issues for approved gaps |
| `/pm:prd` | Generate full PRD and create GitHub Issue |
| `/pm:sync` | Sync local cache with GitHub Issues |

**Features:**
- WINNING prioritization filter (Worth building, Important, New to us, Needed, Implementable, Next step clear, Good for users)
- Competitive research with web search
- GitHub Issues integration with deduplication
- Local `.pm-data/` cache for offline work

**Agents:** gap-analyst, research-agent, prd-generator

---

### jkramer

Personal productivity plugin with meeting notes processing and architecture diagram generation.

#### meeting-notes

Process meeting transcripts into structured Notion entries.

| Command | Description |
|---------|-------------|
| `/meeting-notes` | Process transcript → Notion summary + action items |

**Triggers:** "meeting notes", "process this meeting", "summarize this transcript", or pasting meeting dialogue

**Output:**
- Meeting Notes page with comprehensive, topic-organized notes
- Action items (To-Do entries) with assignees, due dates, priorities
- Linked via Notion relation fields
- Detailed context in each action item's page body

#### excalidraw

Generate architecture diagrams as `.excalidraw` files from codebase analysis.

**Triggers:** "architecture diagram", "excalidraw", "visualize codebase", "system diagram"

**Features:**
- Analyzes any codebase (any language/framework)
- Generates valid Excalidraw JSON with proper bindings and arrow routing
- Semantic color palettes for component types (frontend, backend, database, etc.)
- Optional PNG/SVG export via Playwright MCP

---

## Standalone Skills

### uat-testing

End-to-end User Acceptance Testing for web applications.

**Triggers:** "run UAT", "test this feature", "acceptance test", "test my branch"

**Workflow:**
1. **Discovery** — Reads spec/requirements, analyzes git branch diff
2. **Environment Setup** — Starts dev server or connects to staging URL, requests test credentials
3. **Test Case Generation** — Writes `uat-test-cases.md` covering happy path, errors, persistence, auth
4. **Execution** — Runs tests via Playwright MCP tools, takes screenshots as evidence
5. **Reporting** — Writes `uat-results.md` with pass/fail verdict, fix documentation

**Templates:** `references/test-case-template.md`, `references/results-template.md`, `references/agent-guide.md`

---

## Quick Reference

```bash
# Product Management
/pm:analyze                    # Understand current product
/pm:landscape                  # Research competitors
/pm:gaps                       # Identify & score gaps
/pm:file                       # Create GitHub Issues
/pm:prd                        # Generate full PRD
/pm:sync                       # Sync with GitHub

# Presentations
/deckling "Topic - N slides"   # Generate PPTX
/deckling "Change X" --refine  # Refine existing deck

# Launch Readiness
/launch-check                  # 10-point audit

# Productivity
/meeting-notes                 # Process transcript
```

---

## Credits

The following plugins are adapted from [ooiyeefei/ccc](https://github.com/ooiyeefei/ccc):
- deckling
- mvp-launch
- product-management

The excalidraw skill originated from the same source and has been enhanced with export capabilities.
