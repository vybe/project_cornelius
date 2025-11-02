# Quick Start (5 Minutes)

Get Claude Code Second Brain running in your Obsidian vault in 5 minutes.

## 1. Prerequisites (2 min)

```bash
# Install Claude Code (if not already installed)
# Visit: https://claude.ai/claude-code

# Verify Node.js
node --version  # Should be 18+

# Install MCP server
npm install -g @modelcontextprotocol/server-obsidian
```

## 2. Install in Vault (1 min)

```bash
# Copy to your vault
cd /path/to/this/template
cp -r .claude CLAUDE.md /path/to/your/vault/
```

## 3. Configure Vault Path (1 min)

Edit `/path/to/your/vault/.claude/settings.md`:

**Change this line:**
```
VAULT_BASE_PATH=/path/to/your/vault
```

**To your actual path:**
```
VAULT_BASE_PATH=/Users/yourname/Documents/YourVault
```

**Then update** `.mcp.json` to match (for Smart Connections MCP)

## 4. Create Folders (30 sec)

```bash
cd /path/to/your/vault
mkdir -p Inbox Permanent MOCs Output Meta/Changelogs
```

## 5. Start & Test (30 sec)

```bash
cd /path/to/your/vault
claude
```

In Claude Code:
```
/search-vault test
```

If this works, you're done! 🎉

## What You Just Installed

### Commands Available
- `/search-vault <query>` - Search your notes
- `/recall <topic>` - Deep semantic search
- `/find-connections <note>` - Discover relationships
- `/analyze-kb` - Generate structure report

### Agents Available
- **vault-manager**: Create/organize notes
- **connection-finder**: Find hidden connections
- **auto-discovery**: Explore cross-domain patterns
- **insight-extractor**: Extract insights from content

## Quick Wins

### Try This Right Now

**Find what you have:**
```
/search-vault [any topic in your vault]
```

**Discover connections:**
```
/find-connections [name of a note you have]
```

**Create your first permanent note:**
```
Can you help me create a permanent note about [idea] in the Permanent/ folder?
```

## Next Steps (When You Have Time)

1. **Read the README** - Understand the system
2. **Check EXAMPLES** - See what good notes look like
3. **Review FOLDER-STRUCTURE** - Organize your vault properly
4. **Install Smart Connections** (Obsidian plugin) - Better semantic search

## Troubleshooting

### "MCP server not found"
```bash
# Check installation
npm list -g @modelcontextprotocol/server-obsidian

# Create MCP config
mkdir -p ~/.config/claude-code
echo '{
  "mcpServers": {
    "obsidian-mcp": {
      "command": "npx",
      "args": ["@modelcontextprotocol/server-obsidian", "/path/to/vault"]
    }
  }
}' > ~/.config/claude-code/mcp_settings.json
```

Replace `/path/to/vault` with your actual path.

### "Permission denied"
- Check `VAULT_BASE_PATH` in `.claude/settings.md`
- Use absolute path (e.g., `/Users/name/vault`)
- Verify folder permissions: `ls -la /path/to/vault`

### Commands not working
- Verify files in `.claude/commands/` exist
- Restart Claude Code

## What's Next?

**Start simple:**
1. Create notes in `Permanent/`
2. Run `/find-connections` to see relationships
3. Create your first MOC when you have 10+ related notes

**Explore gradually:**
- Read EXAMPLES.md for note templates
- Try agents when you need them
- Build your system over time

## Full Documentation

- **README.md** - Complete overview
- **INSTALL.md** - Detailed installation
- **EXAMPLES.md** - Sample notes and workflows
- **FOLDER-STRUCTURE.md** - Organization guide
- **MCP-SETUP.md** - Advanced MCP configuration

---

**You're ready to go!** Start with `/search-vault` and explore from there.
