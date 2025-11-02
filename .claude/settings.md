---
description: Centralized configuration settings for the knowledge management system
---

# Configuration Variables

## Vault Paths

VAULT_BASE_PATH=/path/to/your/vault

## MCP Configuration

SMART_VAULT_PATH=/path/to/your/vault

## Directory Paths (relative to VAULT_BASE_PATH)

BRAIN_DIR=Brain
INBOX_DIR=Brain/00-Inbox
SOURCES_DIR=Brain/01-Sources
PERMANENT_NOTES_DIR=Brain/02-Permanent
MOCS_DIR=Brain/03-MOCs
OUTPUT_DIR=Brain/04-Output
META_DIR=Brain/05-Meta
CHANGELOGS_DIR=Brain/05-Meta/Changelogs
AI_EXTRACTED_DIR=Brain/AI Extracted Notes

---

**Setup Instructions**:
1. Replace `/path/to/your/vault` with your actual vault path
2. Update `.mcp.json` - set `SMART_VAULT_PATH` to match
3. Update `settings.local.json` - set Bash permission to match
4. Restart Claude Code to apply changes

**Examples**:
- macOS: `/Users/yourusername/Dropbox/YourVault`
- Windows: `C:/Users/yourusername/Documents/YourVault`
- Linux: `/home/yourusername/Documents/YourVault`
