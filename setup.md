# Layer Bookkeeper MCP Setup

Connect to the Layer Bookkeeper MCP server to enable bookkeeping capabilities in Claude.

## Quick Setup (Recommended)

Run this command in your terminal, replacing `YOUR_API_KEY` with the key provided by Layer:

```bash
claude mcp add layer-bookkeeper --transport sse --url https://bookkeeping-mcp.layerfi.com/sse --header "X-API-Key: YOUR_API_KEY"
```

Then restart Claude Desktop.

## Getting Your API Key

Contact Layer to obtain your API key for the hosted MCP server.

## Verifying Connection

After setup:

1. Restart Claude Desktop
2. Start a new conversation
3. Ask: "List available Layer businesses"

If configured correctly, Claude will query the MCP server and return your businesses.

## Manual Setup (Alternative)

If the CLI command doesn't work, manually edit your Claude Desktop config:

**macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "layer-bookkeeper": {
      "transport": {
        "type": "sse",
        "url": "https://bookkeeping-mcp.layerfi.com/sse",
        "headers": {
          "X-API-Key": "YOUR_API_KEY"
        }
      }
    }
  }
}
```

## What's Included

Once connected, you'll have access to:

- **Journal Entries** - Create, view, and manage custom journal entries
- **Chart of Accounts** - View and update ledger accounts
- **Financial Reports** - Generate P&L and Balance Sheet reports
- **Transaction Categorization** - Categorize bank transactions
- **Business Management** - List and manage Layer businesses

## Troubleshooting

### "Connection refused" or timeout errors
- Verify your API key is correct
- Check that the URL is exactly as shown above
- Ensure you have internet connectivity

### "Unauthorized" errors
- Double-check your API key
- Contact Layer if your key may have expired

### MCP server not appearing in Claude
- Restart Claude Desktop completely
- Run `claude mcp list` to verify it was added
- Check Claude Desktop logs for errors

## Removing the MCP Server

```bash
claude mcp remove layer-bookkeeper
```
