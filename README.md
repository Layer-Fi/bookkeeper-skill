# Layer Bookkeeper Plugin for Claude Code

A Claude Code plugin that enables AI-assisted bookkeeping using the Layer Finance API.

## Installation

```bash
claude plugin add https://github.com/Layer-Fi/bookkeeper-skill
```

## Setup

After installing the plugin, connect to the Layer MCP server:

```bash
claude mcp add layer-bookkeeper --transport sse --url https://bookkeeping-mcp.layerfi.com/sse --header "X-API-Key: YOUR_API_KEY"
```

Then restart Claude Desktop.

See [setup.md](skills/bookkeeper/setup.md) for detailed instructions.

## Getting Your API Key

Contact Layer Finance to obtain your API key for the hosted MCP server.

## What This Plugin Does

The Layer Bookkeeper plugin teaches Claude how to:

- Create and manage journal entries with proper accounting principles
- Navigate the chart of accounts using stable names
- Generate financial reports (P&L, Balance Sheet)
- Categorize transactions
- Handle PC/MSO entity tagging for medical spas
- Process bulk operations with idempotency

## Key Features

- **Two-Step Change Protocol** - All mutations require explicit user approval
- **Graphical Previews** - Journal entries displayed in clear, readable formats
- **Before/After Reporting** - Financial impact shown after each change
- **Bulk Operations** - Idempotent batch processing with external IDs

## Files

```
.claude-plugin/
└── plugin.json           # Plugin manifest

skills/bookkeeper/
├── SKILL.md              # Core skill instructions
├── accounts-reference.md # Account identifiers and stable names
└── setup.md              # MCP server setup guide
```

## Support

Contact Layer Finance for API access and support.
