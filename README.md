# Layer Bookkeeper Skill for Claude Code

A Claude Code skill that enables AI-assisted bookkeeping using the Layer Finance API.

## Installation

### Claude Code CLI

```bash
claude skill add https://github.com/Layer-Fi/bookkeeper-skill
```

### Manual Installation

Copy the skill files to your Claude skills directory:
- `SKILL.md` - Main skill definition
- `accounts-reference.md` - Account types and stable names
- `setup.md` - MCP server connection guide

## Prerequisites

1. **MCP Server Access** - You need an API key for the Layer Bookkeeper MCP server
2. **Claude Desktop** - Configure the MCP connection (see `setup.md`)

## What This Skill Does

The Layer Bookkeeper skill teaches Claude how to:

- Create and manage journal entries with proper accounting principles
- Navigate the chart of accounts using stable names
- Generate financial reports (P&L, Balance Sheet)
- Categorize transactions
- Handle PC/MSO entity tagging for medical spas
- Process bulk operations with idempotency

## Key Features

### Two-Step Change Protocol
All mutations require explicit user approval before execution.

### Graphical Previews
Journal entries and account changes are displayed in clear, readable formats.

### Before/After Reporting
Financial impact is shown after each change.

## Files

| File | Description |
|------|-------------|
| `SKILL.md` | Core skill instructions and workflows |
| `accounts-reference.md` | Account identifiers, stable names, debit/credit rules |
| `setup.md` | MCP server connection configuration |

## Support

Contact Layer Finance for API access and support.
