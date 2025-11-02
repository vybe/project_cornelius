# Installation Guide

Quick start guide to get the Claude Code Second Brain system running in your Obsidian vault.

## Prerequisites Checklist

- [ ] [Claude Code](https://claude.ai/claude-code) installed
- [ ] [Obsidian](https://obsidian.md/) with an existing vault
- [ ] Node.js 18+ installed (`node --version`)
- [ ] npm or yarn installed (`npm --version`)

## Installation Steps

### Step 1: Copy Files to Your Vault

```bash
# Navigate to this template directory
cd /path/to/claude-second-brain-template

# Copy .claude directory to your vault
cp -r .claude /path/to/your/vault/

# Copy CLAUDE.md to your vault
cp CLAUDE.md /path/to/your/vault/

# Copy documentation (optional but recommended)
cp README.md MCP-SETUP.md FOLDER-STRUCTURE.md EXAMPLES.md /path/to/your/vault/
```

### Step 2: Configure Vault Path

1. **Edit settings.md:**
   ```bash
   # Open in your editor
   code /path/to/your/vault/.claude/settings.md
   # or
   nano /path/to/your/vault/.claude/settings.md
   ```

2. **Update VAULT_BASE_PATH:**
   Change this line:
   ```
   VAULT_BASE_PATH=/path/to/your/vault
   ```

   To your actual vault path:
   ```
   VAULT_BASE_PATH=/Users/yourname/Documents/YourVault
   ```

That's it! All agents and commands will use this path automatically.

### Step 3: Install MCP Servers

#### Install obsidian-mcp
```bash
npm install -g @modelcontextprotocol/server-obsidian
```

Verify:
```bash
npm list -g @modelcontextprotocol/server-obsidian
```

#### Install smart-connections (via Obsidian)
1. Open Obsidian
2. Settings → Community Plugins
3. Browse → Search "Smart Connections"
4. Install → Enable
5. Configure in plugin settings:
   - Set embedding model (recommended: `TaylorAI/bge-micro-v2`)
   - Choose folders to index
   - Run initial indexing

For detailed MCP setup, see [MCP-SETUP.md](MCP-SETUP.md)

### Step 4: Configure MCP Connection

Create or edit MCP settings file:

**Linux/Mac:**
```bash
mkdir -p ~/.config/claude-code
nano ~/.config/claude-code/mcp_settings.json
```

**Windows:**
```cmd
mkdir %APPDATA%\claude-code
notepad %APPDATA%\claude-code\mcp_settings.json
```

**Add this configuration:**
```json
{
  "mcpServers": {
    "obsidian-mcp": {
      "command": "npx",
      "args": [
        "@modelcontextprotocol/server-obsidian",
        "/path/to/your/vault"
      ]
    }
  }
}
```

Replace `/path/to/your/vault` with your actual vault path.

### Step 5: Create Folder Structure

Create recommended folders in your vault:

```bash
cd /path/to/your/vault

# Create core folders
mkdir -p Inbox/Quick\ Captures
mkdir -p Inbox/Content\ Extractions
mkdir -p Sources/Books
mkdir -p Sources/Articles
mkdir -p Permanent
mkdir -p MOCs
mkdir -p Output/Articles
mkdir -p Output/Frameworks
mkdir -p Output/Insights
mkdir -p Meta/Changelogs
mkdir -p Meta/Templates
mkdir -p "AI Extracted Notes"
```

Or create them in Obsidian's UI.

For detailed folder structure, see [FOLDER-STRUCTURE.md](FOLDER-STRUCTURE.md)

### Step 6: Start Claude Code

```bash
cd /path/to/your/vault
claude
```

### Step 7: Test Installation

Try these commands to verify everything works:

```bash
# Test semantic search
/search-vault knowledge management

# Test stats
Can you show me statistics about my vault using smart-connections?

# Test note listing
Can you list some notes in my vault using obsidian-mcp?
```

If any command fails, see [Troubleshooting](#troubleshooting) below.

## Verification Checklist

- [ ] Claude Code starts in your vault directory
- [ ] `/search-vault` command works
- [ ] Semantic search returns results
- [ ] Can list notes with obsidian-mcp
- [ ] Can read notes with obsidian-mcp
- [ ] Agent prompts load (try `/find-connections`)
- [ ] Folder structure created

## Troubleshooting

### Claude Code Not Finding MCP Servers

**Issue**: `MCP server 'obsidian-mcp' not found`

**Solutions**:
1. Verify MCP servers installed: `npm list -g @modelcontextprotocol/server-obsidian`
2. Check `~/.config/claude-code/mcp_settings.json` exists and has correct paths
3. Restart Claude Code
4. Check Claude Code logs for errors

### Permission Denied Errors

**Issue**: `Permission denied reading vault`

**Solutions**:
1. Check `VAULT_BASE_PATH` in `.claude/settings.md` is correct
2. Verify file system permissions: `ls -la /path/to/vault`
3. Ensure path is absolute (e.g., `/Users/name/vault`)

### Smart Connections Not Working

**Issue**: Searches return no results

**Solutions**:
1. Open Obsidian → Smart Connections settings
2. Click "Rebuild Index"
3. Wait for indexing (check progress in Obsidian)
4. Verify folders are configured in plugin settings
5. Check plugin is enabled

### Commands Not Found

**Issue**: `/search-vault: command not found`

**Solutions**:
1. Verify command files exist in `.claude/commands/`
2. Check file names are correct (e.g., `search-vault.md`, not `search-vault`)
3. Restart Claude Code
4. Try absolute path: check if slash command files are in the right location

### Agents Not Working

**Issue**: Agent prompts don't load

**Solutions**:
1. Verify agent files exist in `.claude/agents/`
2. Check paths in agent files are updated to your vault
3. Verify markdown syntax is correct in agent files
4. Restart Claude Code

## Post-Installation

### Optional Enhancements

1. **Configure Git** (recommended for version control):
   ```bash
   cd /path/to/your/vault
   git init
   git add .claude/ CLAUDE.md
   git commit -m "Add Claude Code second brain setup"

   # Add .gitignore
   echo ".claude/settings.local.json" >> .gitignore
   echo ".obsidian/workspace*" >> .gitignore
   ```

2. **Install files-vectorstore** (optional, for broader search):
   ```bash
   npm install -g @lishenxydlgzs/simple-files-vectorstore
   ```

3. **Create templates** in `Meta/Templates/`:
   - Permanent note template
   - Source note template
   - MOC template

4. **Create first MOC**:
   - `MOC - Master Navigation.md`
   - Use example from EXAMPLES.md

### Next Steps

1. **Read documentation**:
   - [README.md](README.md) - Overview and use cases
   - [EXAMPLES.md](EXAMPLES.md) - Sample notes and workflows
   - [FOLDER-STRUCTURE.md](FOLDER-STRUCTURE.md) - Organization guide

2. **Try commands**:
   - `/search-vault [topic]` - Search your vault
   - `/find-connections [note]` - Discover relationships
   - `/analyze-kb` - Generate structure report

3. **Create first notes**:
   - Add a note to `Permanent/`
   - Try `/find-connections` on it
   - Review the connection suggestions

4. **Launch first agent**:
   ```
   Please launch the connection-finder agent to analyze my note on [topic]
   ```

5. **Review examples**:
   - See EXAMPLES.md for note templates
   - Copy and adapt to your needs

## Getting Help

- **Documentation errors**: Check file paths are correct
- **MCP issues**: See MCP-SETUP.md for detailed troubleshooting
- **Workflow questions**: See EXAMPLES.md for workflows
- **Customization**: See CUSTOMIZATION.md (if you created it)

## Updating

To update the system:

1. **Backup current setup**:
   ```bash
   cp -r /path/to/vault/.claude /path/to/vault/.claude.backup
   ```

2. **Download new version** of template

3. **Compare changes**:
   ```bash
   diff -r .claude.backup .claude
   ```

4. **Merge updates** carefully, preserving your customizations

## Uninstalling

To remove:

```bash
cd /path/to/your/vault
rm -rf .claude/
rm CLAUDE.md
# Optionally remove created folders
```

---

**Need more help?** Check the documentation files or review agent prompts in `.claude/agents/` for detailed instructions.

**Ready to start?** Try: `/search-vault second brain` to see what's in your vault!
