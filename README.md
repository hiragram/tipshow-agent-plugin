# tipshow-agent-plugin

Claude Code plugins curated by the tipshow team.

## Installation

```
/plugin install <plugin-name>@tipshow-agent-plugin
```

Or browse in `/plugin > Discover`

## Structure

```
.claude-plugin/
  marketplace.json     # Plugin catalog
plugins/
  <plugin-name>/
    .claude-plugin/
      plugin.json      # Plugin metadata (required)
    .mcp.json          # MCP server config (optional)
    commands/           # Slash commands (optional)
    agents/             # Agent definitions (optional)
    skills/             # Skill definitions (optional)
    hooks/              # Hook definitions (optional)
    README.md           # Documentation
```

## Adding a Plugin

1. Create a directory under `plugins/<plugin-name>/`
2. Add `.claude-plugin/plugin.json` with metadata
3. Add plugin contents (skills, commands, agents, MCP config, etc.)
4. Register the plugin in `.claude-plugin/marketplace.json`
