---
description: Analyze knowledge base structure and update the knowledge-base-analysis.md report
---

Analyze the Obsidian knowledge base structure and regenerate the comprehensive analysis report.

Follow these steps:

1. Get vault statistics using `mcp__smart-connections__get_stats`
2. List all notes with full directory tree using `Bash` find:
   ```bash
   find /path/to/your/vault -name "*.md" -type f | head -50
   ```
3. Use `Glob` to explore directory structure:
   - All notes: `Brain/**/*.md`
   - Permanent notes: `Brain/02-Permanent/*.md`
   - MOCs: `Brain/03-MOCs/*.md`
   - Sources: `Brain/01-Sources/**/*.md`
4. Read key hub notes from major clusters using `Read` tool (Dopamine, Self/Buddhism, Decision-Making, Flow, etc.)
5. Use `mcp__smart-connections__get_similar_notes` to identify highly connected notes
6. Use `mcp__smart-connections__get_connection_graph` to map relationship networks
7. Analyze thematic clusters, hierarchical organization, and conceptual architecture
8. Use `Edit` or `Write` to update the `knowledge-base-analysis.md` file with:
   - Executive summary with key statistics
   - Hierarchical structure mapping
   - 6 major thematic hubs with hub nodes
   - Network properties and connectivity
   - Content topology and source analysis
   - Intellectual trajectory and maturity assessment
   - Recommendations for enhancement

Generate a comprehensive, structured report that reveals the knowledge base's personality, cognitive fingerprint, and growth opportunities.
