# Wikidata Brief Enrichment

Agent skill for enriching Executive Intelligence Briefs (EIBs) with Wikidata references. Designed as a companion to the [MacronX](https://github.com/macron1-automations/macronx) News Analysis workflow.

## What it does

Parses a briefing or intelligence document, resolves named entities to Wikidata QIDs via a local QLever endpoint, and produces an enhanced document with:

- **Inline QID tags** on first entity mention (e.g. `Russia \`Q159\``)
- **Wikidata grounding** lines under each claim tying entities to verified triples
- **Entity catalog** with resolution flags for unresolvable mentions
- **Cross-references** between entities via shared Wikidata relations

## How it fits with MacronX

This skill pairs with the [News Analysis workflow](https://github.com/macron1-automations/macronx#news-analysis) in [macronx](https://github.com/macron1-automations/macronx).

After the pipeline generates an EIB, an analyst can use a coding agent (OpenCode, Cursor, Claude Code, etc.) with this skill to add Wikidata grounding to the brief — turning raw intelligence into a referenceable artifact with verified entity links.

The skill is agent-agnostic and works with any coding agent that supports the [Agent Skills](https://agentskills.io) specification.

## Prerequisites

- **QLever Wikidata endpoint** running on `localhost:7001`
  - English-only, ~2.9B best-rank triples, no qualifiers/references
  - The skill's technical notes include endpoint health checks and query patterns
- A coding agent with [Agent Skills](https://agentskills.io) support (OpenCode, Claude Code, Cursor, Codex, Gemini CLI, etc.)

## Install

### Quick install (all agents)

```bash
npx skills add macron1-automations/wikidata-brief-enrich -g
```

### Install to specific agent(s)

```bash
# OpenCode only
npx skills add macron1-automations/wikidata-brief-enrich -a opencode -g

# Claude Code only
npx skills add macron1-automations/wikidata-brief-enrich -a claude-code -g

# Multiple agents
npx skills add macron1-automations/wikidata-brief-enrich -a opencode -a claude-code -a cursor -g
```

### Project-level install (committed with repo)

```bash
npx skills add macron1-automations/wikidata-brief-enrich -a opencode
```

### Non-interactive install (CI/CD friendly)

```bash
npx skills add macron1-automations/wikidata-brief-enrich -g -a '*' -y
```

### List available before installing

```bash
npx skills add macron1-automations/wikidata-brief-enrich --list
```

### Uninstall

```bash
npx skills remove wikidata-brief-enrich -g
```

## Where it installs

| Scope | Flag | Location |
|-------|------|----------|
| Project (default) | none | `.agents/skills/wikidata-brief-enrich/SKILL.md` |
| Global | `-g` | `~/.config/opencode/skills/wikidata-brief-enrich/SKILL.md` |

The skill installs to all supported agent directories by default. See below for the full list of compatible agents.

## Supported agents

| Agent | Install command |
|-------|----------------|
| OpenCode | `npx skills add macron1-automations/wikidata-brief-enrich -a opencode` |
| Claude Code | `npx skills add macron1-automations/wikidata-brief-enrich -a claude-code` |
| Cursor | `npx skills add macron1-automations/wikidata-brief-enrich -a cursor` |
| Codex | `npx skills add macron1-automations/wikidata-brief-enrich -a codex` |
| Gemini CLI | `npx skills add macron1-automations/wikidata-brief-enrich -a gemini-cli` |
| Kiro CLI | `npx skills add macron1-automations/wikidata-brief-enrich -a kiro-cli` |
| Roo Code | `npx skills add macron1-automations/wikidata-brief-enrich -a roo` |
| Continue | `npx skills add macron1-automations/wikidata-brief-enrich -a continue` |
| GitHub Copilot | `npx skills add macron1-automations/wikidata-brief-enrich -a github-copilot` |
| All agents | `npx skills add macron1-automations/wikidata-brief-enrich -a '*'` |

The CLI supports 75+ agents. Run `npx skills list -a <agent>` after install to verify.

## Usage

1. Open a coding agent (e.g. OpenCode) with this skill installed
2. Paste or reference a briefing / intelligence document
3. Trigger the skill with: *"extract entities, enrich with Wikidata"*
4. The agent resolves entities via the local QLever endpoint and returns an enhanced document with QID tags and Wikidata grounding

## License

MIT
