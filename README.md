# Project Cornelius

**AI-powered second brain template for Claude Code + Obsidian**

Capture insights, discover connections, and synthesize knowledge—with AI assistance.

---

## 🚀 Quick Start

```bash
# 1. Clone this repository
git clone https://github.com/vybe/project_cornelius.git
cd project_cornelius

# 2. Configure your vault path
cp .claude/settings.md.template .claude/settings.md
# Edit .claude/settings.md and set your vault path:
# VAULT_BASE_PATH=/path/to/your/vault

# 3. Configure MCP servers
# Edit .mcp.json and update all vault paths to match your vault
# Or use: /switch-brain /path/to/your/vault

# 4. Start Claude Code
claude
```

→ **[QUICKSTART.md](QUICKSTART.md)** for 5-minute setup
→ **[INSTALL.md](INSTALL.md)** for detailed installation
→ **[MCP-SETUP.md](MCP-SETUP.md)** for MCP server configuration (required)

---

## 📁 What's Included

### AI Agents (`.claude/agents/`)
- **vault-manager** - Create and organize notes
- **connection-finder** - Find hidden relationships
- **auto-discovery** - Discover cross-domain patterns
- **insight-extractor** - Extract insights from content
- **diagram-generator** - Create visualizations

### Commands (`.claude/commands/`)
- `/search-vault <query>` - Quick search
- `/recall <topic>` - Deep 3-layer semantic search
- `/find-connections <note>` - Discover relationships
- `/analyze-kb` - Generate structure report
- `/switch-brain <path>` - Switch to different vault

### Sample Vault (`Brain/`)
Complete folder structure with templates:
- `00-Inbox/` - Capture zone
- `01-Sources/` - Books, articles, videos
- `02-Permanent/` - Your atomic insights (core)
- `03-MOCs/` - Navigation hubs
- `04-Output/` - Articles, frameworks, insights
- `05-Meta/` - Changelogs, templates

---

## 📖 Documentation

| File | Purpose |
|------|---------|
| **[QUICKSTART.md](QUICKSTART.md)** | 5-minute setup |
| **[INSTALL.md](INSTALL.md)** | Detailed installation & troubleshooting |
| **[EXAMPLES.md](EXAMPLES.md)** | Sample notes, MOCs, workflows |
| **[FOLDER-STRUCTURE.md](FOLDER-STRUCTURE.md)** | Vault organization guide |
| **[MCP-SETUP.md](MCP-SETUP.md)** | MCP server configuration |
| **[Brain/README.md](Brain/README.md)** | Sample vault guide |

---

## 🎯 Use Cases

**Capture**: Extract insights from books and articles
**Connect**: Find non-obvious relationships between ideas
**Create**: Synthesize notes into articles and frameworks
**Evolve**: Track how your thinking changes over time

---

## 💡 Core Principles

**Atomic notes** - One idea per note
**Your words** - Not copy-paste from sources
**Rich links** - Connect everything
**Regular discovery** - Find patterns with agents
**Active synthesis** - Create from connections

---

## 🛠️ Requirements

- [Claude Code](https://claude.ai/claude-code)
- [Obsidian](https://obsidian.md/)
- Node.js 18+
- MCP servers (via npm)

---

## 📝 License

MIT - Use, modify, distribute freely. See [LICENSE](LICENSE).

---

**Questions?** Check the docs above or start with **[QUICKSTART.md](QUICKSTART.md)** 🧠✨
