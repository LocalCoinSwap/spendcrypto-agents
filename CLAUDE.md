# SpendCrypto Skills — Agent Guide

Monorepo of agent skills for SpendCrypto, packaged as a Claude Code / Cowork plugin marketplace.

## Install

```bash
/plugin marketplace add spendcrypto/spendcrypto-agents
/plugin install spendcrypto@spendcrypto-skills
/reload-plugins
```

Bundled MCP: `.mcp.json` → `https://api.spendcrypto.com/mcp` (OAuth on first call in Claude Code).

## Structure

```
.claude-plugin/   plugin.json, marketplace.json
.mcp.json         MCP server definition
skills/           one directory per skill (SKILL.md required)
```

## Adding a skill

1. `skills/<name>/SKILL.md` with YAML frontmatter (`name`, `description`)
2. Optional `references/`
3. Bump `version` in `.claude-plugin/plugin.json` and `marketplace.json`

Skill `name` must match directory name (lowercase, hyphens).

## Publish

After edits: bump version, validate, push tag/release as needed.

```bash
claude plugin validate .
```
