# MCP Server Setup Guide

This guide covers installation and configuration of MCP (Model Context Protocol) servers for Claude Code integration with your Obsidian workspace.

## Overview

MCP servers enable Claude Code to interact with your Obsidian workspace programmatically. This template uses:

1. **obsidian-mcp**: Direct workspace operations (CRUD, search, tags)
2. **smart-connections**: Semantic search and similarity analysis
3. **files-vectorstore** (optional): Broad file system search

**IMPORTANT**: MCP servers should point to your Obsidian **workspace folder** (the folder containing `.obsidian/` directory), NOT individual vault subfolders. This allows you to:
- Work with multiple vaults in one workspace
- Access the Obsidian configuration
- Switch between different vault contexts seamlessly

## Prerequisites

- Node.js 18 or higher
- npm or yarn package manager
- Obsidian workspace with notes (folder containing `.obsidian/` directory)
- Claude Code installed

## Installation

### 1. Install obsidian-mcp

```bash
npm install -g @modelcontextprotocol/server-obsidian
```

Or using yarn:
```bash
yarn global add @modelcontextprotocol/server-obsidian
```

**Verify installation:**
```bash
npm list -g @modelcontextprotocol/server-obsidian
```

### 2. Install smart-connections (Recommended)

Smart Connections is an Obsidian plugin that provides semantic search capabilities.

**Option A: Through Obsidian (Recommended)**
1. Open Obsidian Settings
2. Go to Community Plugins
3. Browse and search for "Smart Connections"
4. Install and enable

**Option B: Manual Installation**
1. Download from: https://github.com/brianpetro/obsidian-smart-connections
2. Extract to `.obsidian/plugins/smart-connections/`
3. Enable in Obsidian settings

**Configure Smart Connections:**
1. Open plugin settings in Obsidian
2. Set embedding model (recommended: `TaylorAI/bge-micro-v2`)
3. Configure folders to index
4. Run initial indexing

### 3. Install files-vectorstore (Optional)

For broader file system search beyond Obsidian notes:

```bash
npm install -g @lishenxydlgzs/simple-files-vectorstore
```

## Configuration

### Configure Claude Code Permissions

**CRITICAL**: Create `.claude/settings.local.json` (NOT in project root):

```bash
# From project root
cp .claude/settings.local.json.template .claude/settings.local.json
```

Edit `.claude/settings.local.json`:

```json
{
  "permissions": {
    "allow": [
      "Bash(node --version:*)",
      "Bash(npm --version)",
      "WebSearch",
      "mcp__smart-connections__get_stats",
      "mcp__smart-connections__search_notes",
      "mcp__smart-connections__get_similar_notes",
      "mcp__smart-connections__get_connection_graph",
      "mcp__smart-connections__get_note_content"
    ],
    "deny": [],
    "ask": []
  },
  "enableAllProjectMcpServers": true,
  "enabledMcpjsonServers": [
    "smart-connections"
  ]
}
```

**NOTE**: This file grants permissions for MCP tools. Workspace paths are configured separately in `.mcp.json` and `.claude/settings.md`.

### Configure MCP Server Connection

Claude Code needs to know how to connect to your MCP servers. This is typically configured in your global Claude Code settings.

**Location**: `~/.config/claude-code/mcp_settings.json` (or equivalent for your OS)

**Example configuration:**

```json
{
  "mcpServers": {
    "obsidian-mcp": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-obsidian",
        "/path/to/your/workspace"
      ]
    },
    "smart-connections": {
      "command": "node",
      "args": [
        "/path/to/obsidian/.obsidian/plugins/smart-connections/mcp-server.js",
        "/path/to/your/workspace"
      ]
    }
  }
}
```

**IMPORTANT**: Use your workspace folder path (containing `.obsidian/`), not a vault subfolder.

**Example**:
- ✅ Correct: `/Users/yourname/Dropbox/Cornelius`
- ❌ Wrong: `/Users/yourname/Dropbox/Cornelius/Brain`

## Verification

### Test obsidian-mcp

```bash
# List notes
claude-mcp obsidian-mcp obsidian_list_notes '{"folder": ""}'

# Read a note
claude-mcp obsidian-mcp obsidian_read_note '{"notePath": "YourNote.md"}'
```

### Test smart-connections

In Claude Code:
```
Can you search my notes for "knowledge management"?
```

Claude should use `mcp__smart-connections__search_notes` to find relevant notes.

### Test Integration

In Claude Code:
```
/search-vault knowledge management
```

This command uses both MCP servers to provide comprehensive search results.

## Troubleshooting

### MCP Server Not Found

**Error**: `MCP server 'obsidian-mcp' not found`

**Solution**:
1. Verify installation: `npm list -g @modelcontextprotocol/server-obsidian`
2. Check MCP settings in `~/.config/claude-code/mcp_settings.json`
3. Restart Claude Code

### Permission Denied

**Error**: `Permission denied reading workspace`

**Solution**:
1. Check workspace path in `.claude/settings.local.json`
2. Ensure `Read(//path/to/workspace/**)` is in permissions.allow
3. Verify path points to workspace folder (with `.obsidian/`), not vault subfolder
4. Verify file system permissions on workspace directory: `ls -la /path/to/workspace`

### Smart Connections Not Indexing

**Problem**: Searches return no results

**Solution**:
1. Open Obsidian
2. Go to Smart Connections settings
3. Click "Rebuild Index"
4. Wait for indexing to complete
5. Check that folders are configured correctly

### Connection Timeout

**Error**: `MCP server connection timeout`

**Solution**:
1. Check that MCP server process is running
2. Verify network/socket permissions
3. Check server logs for errors
4. Restart Claude Code

## Performance Optimization

### For Large Workspaces (1000+ notes)

1. **Smart Connections**:
   - Use lighter embedding model
   - Exclude large folders from indexing
   - Index only markdown files
   - Configure specific vault folders if workspace contains multiple vaults

2. **obsidian-mcp**:
   - Use specific folder paths in commands
   - Limit search results
   - Cache frequently accessed notes

3. **files-vectorstore**:
   - Adjust chunk size (default: 1000 chars)
   - Configure watch directories carefully
   - Use file type filters

## Advanced Configuration

### Custom Similarity Thresholds

Edit agent files in `.claude/agents/` to adjust:

```markdown
- connection-finder: 0.65-0.95 (moderate to strong)
- auto-discovery: 0.50-0.70 (weak to moderate)
```

Lower threshold = more connections, less relevance
Higher threshold = fewer connections, more relevance

### Multiple Vaults in One Workspace

Obsidian workspaces can contain multiple vaults as subfolders. To work with this setup:

1. Point MCP servers to the workspace folder (parent containing `.obsidian/`)
2. The workspace can access all vaults within it
3. Use `/switch-brain` to point to different workspace folders if working with completely separate workspaces
4. Organize workspace structure like:
   ```
   /Workspace/
     .obsidian/          # Main Obsidian config
     Vault1/             # First vault
     Vault2/             # Second vault
     *.md files          # Or files directly in workspace
   ```

### Custom MCP Servers

To add custom MCP servers:

1. Install the server package
2. Add to `mcp_settings.json`
3. Add permissions to `.claude/settings.local.json`
4. Reference in agent/command prompts

## Security Considerations

### Permissions

- Grant minimal permissions needed
- Use specific paths, not wildcards when possible
- Review permissions regularly
- Never commit `settings.local.json` with sensitive paths

### API Keys

If using external services:
- Store API keys in environment variables
- Never commit keys to git
- Use `.env` files with `.gitignore`

### Network Access

- MCP servers run locally by default
- No data sent to external servers (unless using cloud embedding models)
- Review plugin code before installation

## Updating

### Update obsidian-mcp
```bash
npm update -g @modelcontextprotocol/server-obsidian
```

### Update smart-connections
1. Open Obsidian
2. Go to Community Plugins
3. Check for updates
4. Update if available
5. Restart Obsidian

### Update files-vectorstore
```bash
npm update -g @lishenxydlgzs/simple-files-vectorstore
```

## Resources

- [MCP Documentation](https://modelcontextprotocol.io/)
- [Obsidian MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/obsidian)
- [Smart Connections Plugin](https://github.com/brianpetro/obsidian-smart-connections)
- [Claude Code Documentation](https://docs.anthropic.com/claude/claude-code)

## Getting Help

1. Check error messages in Claude Code
2. Review MCP server logs
3. Verify configurations in this guide
4. Test each component separately
5. Check Obsidian console for plugin errors

---

Once MCP servers are set up, return to the main README.md to continue with folder structure and usage.
