---
description: Switch to a different Obsidian vault (Brain) by updating configuration files
argument-hint: <full path to vault>
allowed-tools: Read, Edit
---

# Switch Brain Command

Switch the active Obsidian vault by updating all configuration files to point to a new vault path.

## New Vault Path
$ARGUMENTS

## Instructions

1. **Validate the path format:**
   - Ensure $ARGUMENTS is a full absolute path
   - If the path looks invalid or incomplete, ask the user to provide the full path

2. **Update `.claude/settings.md`:**
   - Read the file at `/Users/eugene/Dropbox/Coding/project_cornelius/.claude/settings.md`
   - Replace the `VAULT_BASE_PATH=` value with: `VAULT_BASE_PATH=$ARGUMENTS`
   - Use the Edit tool to make this change

3. **Update `.mcp.json`:**
   - Read the file at `/Users/eugene/Dropbox/Coding/project_cornelius/.mcp.json`
   - Find all vault path references in both the `obsidian-mcp` and `smart-connections` server configurations
   - Replace all old vault paths with: `$ARGUMENTS`
   - Use the Edit tool to update all occurrences (there should be 3 total):
     - Line for obsidian-mcp args
     - Line for smart-connections plugin path (append `/.obsidian/plugins/smart-connections/mcp-server.js`)
     - Line for smart-connections vault path

4. **Confirm completion:**
   - Display a summary of what was changed
   - Show the new vault path that's now configured
   - **IMPORTANT**: Display this final message to the user:

```
✅ Vault configuration updated successfully!

New vault path: $ARGUMENTS

⚠️  RESTART REQUIRED: You must restart Claude Code for these changes to take effect.

The MCP servers (obsidian-mcp and smart-connections) will connect to the new vault after restart.
```

## Notes
- This command updates both the settings and MCP server configuration
- Changes only take effect after restarting Claude Code
- Make sure the specified vault path exists and contains a `.obsidian` folder
