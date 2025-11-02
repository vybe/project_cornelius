---
description: Switch to a different Obsidian workspace by updating configuration files
argument-hint: <full path to workspace>
allowed-tools: Read, Edit
---

# Switch Brain Command

Switch the active Obsidian workspace by updating all configuration files to point to a new workspace path.

**IMPORTANT**: This should point to your Obsidian **workspace folder** (containing `.obsidian/` directory), NOT individual vault subfolders.

## New Workspace Path
$ARGUMENTS

## Instructions

1. **Validate the path format:**
   - Ensure $ARGUMENTS is a full absolute path
   - **CRITICAL**: Verify the path points to a workspace folder (should contain `.obsidian/` directory), NOT a vault subfolder
   - If the path looks like it's pointing to a vault subfolder (e.g., `/path/Brain`), warn the user and ask them to provide the parent workspace path instead
   - If the path looks invalid or incomplete, ask the user to provide the full path

2. **Update `.claude/settings.md`:**
   - Read the file at `/Users/eugene/Dropbox/Coding/project_cornelius/.claude/settings.md`
   - Replace the `VAULT_BASE_PATH=` value with: `VAULT_BASE_PATH=$ARGUMENTS`
   - Use the Edit tool to make this change

3. **Update `.mcp.json`:**
   - Read the file at `/Users/eugene/Dropbox/Coding/project_cornelius/.mcp.json`
   - Find all workspace path references in both the `obsidian-mcp` and `smart-connections` server configurations
   - Replace all old workspace paths with: `$ARGUMENTS`
   - Use the Edit tool to update all occurrences:
     - Line for obsidian-mcp args (should be just `$ARGUMENTS`)
     - Line for smart-connections SMART_VAULT_PATH environment variable (should be `$ARGUMENTS`)

4. **Confirm completion:**
   - Display a summary of what was changed
   - Show the new workspace path that's now configured
   - **IMPORTANT**: Display this final message to the user:

```
✅ Workspace configuration updated successfully!

New workspace path: $ARGUMENTS

⚠️  RESTART REQUIRED: You must restart Claude Code for these changes to take effect.

The MCP servers (obsidian-mcp and smart-connections) will connect to the new workspace after restart.

💡 TIP: This workspace folder should contain your .obsidian/ directory. If you have multiple vaults, they should be subfolders within this workspace.
```

## Notes
- This command updates both the settings and MCP server configuration
- Changes only take effect after restarting Claude Code
- **The path must point to the workspace folder (containing `.obsidian/`), NOT a vault subfolder**
- A workspace can contain multiple vaults as subfolders, or markdown files directly within it

## Path Examples
✅ **Correct**: `/Users/yourname/Dropbox/Cornelius` (contains `.obsidian/`)
❌ **Wrong**: `/Users/yourname/Dropbox/Cornelius/Brain` (vault subfolder)
