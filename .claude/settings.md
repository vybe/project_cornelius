---
description: Centralized configuration settings for vault paths and system variables
---

# System Configuration Settings

This file contains centralized configuration settings used throughout the Claude Code system, including agents, commands, and MCP servers.

---

## Vault Configuration

### Primary Vault Path

**VAULT_BASE_PATH**: `/path/to/your/vault`

This is the **base path** to the Obsidian knowledge vault. All agents, commands, and MCP tools reference this path.

**IMPORTANT**: Replace `/path/to/your/vault` with your actual vault path. For example:
- macOS: `/Users/yourusername/Dropbox/YourVaultName`
- Windows: `C:/Users/yourusername/Obsidian/YourVaultName`
- Linux: `/home/yourusername/Documents/YourVaultName`

**Usage in agents and commands:**
- When you need to reference the vault root: `$VAULT_BASE_PATH`
- When you need to reference specific directories: `$VAULT_BASE_PATH/Brain/02-Permanent/`
- When passing to MCP tools: Use `$VAULT_BASE_PATH` directly

**Examples:**
```markdown
# In agent instructions:
- Find notes: `find $VAULT_BASE_PATH/Brain/02-Permanent -name "*.md"`
- List files: `ls "$VAULT_BASE_PATH/Brain/04-Output/Articles/"`
- Read note: `Read` with file_path: `$VAULT_BASE_PATH/Brain/02-Permanent/Note.md`

# In command files:
- Glob pattern: `Brain/02-Permanent/*.md` (relative from $VAULT_BASE_PATH)
- Bash find: `find $VAULT_BASE_PATH -name "*.md" -type f`
```

---

## Directory Structure Reference

**Quick reference** to vault organization (all relative to `$VAULT_BASE_PATH`):

```
$VAULT_BASE_PATH/
├── Brain/                          # Primary intellectual workspace
│   ├── 00-Inbox/                   # Capture & staging
│   │   ├── Quick Captures/         # Fleeting notes
│   │   └── Content Extractions/    # Raw content analysis
│   ├── 01-Sources/                 # Source material
│   │   ├── Books/
│   │   ├── Articles/
│   │   └── Videos/
│   ├── 02-Permanent/               # Atomic insights
│   ├── 03-MOCs/                    # Maps of Content
│   ├── 04-Output/                  # Published content
│   │   ├── Articles/
│   │   ├── LinkedIn Insights/
│   │   ├── Frameworks/
│   │   ├── Projects/
│   │   └── Draft Posts/
│   ├── 05-Meta/                    # System files
│   │   ├── Changelogs/             # Session changelogs
│   │   └── Templates/              # Note templates
│   └── AI Extracted Notes/         # AI-extracted insights
├── Second Brain/                   # Topic-organized knowledge
├── .smart-env/                     # Smart Connections data
├── .claude/                        # Claude Code configuration
│   ├── agents/                     # Specialized agents
│   ├── commands/                   # Custom commands
│   └── settings.md                 # This file
└── CHANGELOG.md                    # Master changelog index
```

**Note**: Adjust this structure to match your vault's organization if different.

---

## MCP Integration

### Smart Connections MCP

Smart Connections MCP uses the **SMART_VAULT_PATH** environment variable, which is configured in `.mcp.json`:

```json
"env": {
  "SMART_VAULT_PATH": "${SMART_VAULT_PATH:-/path/to/your/vault}"
}
```

**IMPORTANT**: When changing `VAULT_BASE_PATH` in this file, you must also update:
1. `.mcp.json` - Update the `SMART_VAULT_PATH` fallback value
2. `settings.local.json` - Update the Bash permission pattern (if using)

**Why two variables?**
- `VAULT_BASE_PATH` - Used in agent/command documentation and references
- `SMART_VAULT_PATH` - Environment variable for Smart Connections MCP server

Both should **always point to the same path**.

**Example .mcp.json configuration**:
```json
{
  "mcpServers": {
    "smart-connections": {
      "type": "stdio",
      "command": "node",
      "args": ["/path/to/smart-connections-mcp/dist/index.js"],
      "env": {
        "SMART_VAULT_PATH": "${SMART_VAULT_PATH:-/path/to/your/vault}",
        "MCP_TRANSPORT_TYPE": "stdio",
        "MCP_LOG_LEVEL": "${MCP_LOG_LEVEL:-info}"
      }
    }
  }
}
```

**Example settings.local.json permission**:
```json
{
  "permissions": {
    "allow": [
      "Bash(SMART_VAULT_PATH=/path/to/your/vault node:*)",
      "mcp__smart-connections__get_stats",
      "mcp__smart-connections__search_notes"
    ]
  }
}
```

---

## Changing Vault Location

**To switch to a different vault:**

1. **Update this file**: Change `VAULT_BASE_PATH` value above
2. **Update `.mcp.json`**: Change `SMART_VAULT_PATH` fallback value
3. **Update `settings.local.json`**: Change Bash permission pattern (if applicable)
4. **Restart Claude Code**: Reload to apply MCP configuration changes

**Example** - Switching to a test vault:
```markdown
# In settings.md:
VAULT_BASE_PATH: /Users/username/Dropbox/TestVault

# In .mcp.json:
"SMART_VAULT_PATH": "${SMART_VAULT_PATH:-/Users/username/Dropbox/TestVault}"

# In settings.local.json:
"Bash(SMART_VAULT_PATH=/Users/username/Dropbox/TestVault node:*)"
```

---

## Additional Configuration Variables

*Reserved for future configuration settings*

---

**Configuration Template**
**Replace `/path/to/your/vault` with your actual vault path**
**Ensure consistency across settings.md, .mcp.json, and settings.local.json**
