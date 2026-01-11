# Layer Bookkeeper MCP Setup

Connect to the Layer Bookkeeper MCP server to enable bookkeeping capabilities in Claude.

## Claude Desktop Configuration

Add to your Claude Desktop MCP configuration:

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

## Getting Access

Contact Layer to obtain your API key for the hosted MCP server.

## What's Included

Once connected, you'll have access to:

- **Journal Entries** - Create, view, and manage custom journal entries
- **Chart of Accounts** - View and update ledger accounts
- **Financial Reports** - Generate P&L and Balance Sheet reports
- **Transaction Categorization** - Categorize bank transactions
- **Business Management** - List and manage Layer businesses

## Verifying Connection

After configuring Claude Desktop:

1. Restart Claude Desktop
2. Start a new conversation
3. Ask: "List available Layer businesses"

If configured correctly, Claude will query the MCP server and return your businesses.

## Troubleshooting

### "Connection refused" or timeout errors
- Verify your API key is correct
- Check that the URL is exactly as shown above
- Ensure you have internet connectivity

### "Unauthorized" errors
- Double-check your X-API-Key header
- Contact Layer if your key may have expired

### MCP server not appearing in Claude
- Ensure the JSON syntax is valid (no trailing commas)
- Restart Claude Desktop completely
- Check Claude Desktop logs for errors
