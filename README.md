# nader

## Banana Claude skill

This repository includes the standalone `banana` Claude Code skill, installed
as a project-scoped skill at `.claude/skills/banana`. It is imported from
[AgriciDaniel/banana-claude](https://github.com/AgriciDaniel/banana-claude)
(MIT License) and enables generating, editing, comparing, and reviewing
Gemini images directly from Claude Code.

### Requirements

- Claude Code 2.1.199 or newer
- Python 3.11 or newer, available as `python3` (standard library only, no
  extra dependencies)
- A Gemini API key for a billing-enabled Google AI project, set as
  `GEMINI_API_KEY` in the environment

### Usage

Once Claude Code loads this project, invoke the skill by describing the
image you want, or run the bundled scripts directly, e.g.:

```bash
python3 .claude/skills/banana/scripts/generate.py --prompt "..."
```

Scripts plan by default; paid execution requires a matching plan plus
`--execute --confirm APPROVAL_ID`. See `.claude/skills/banana/SKILL.md` for
the full workflow, and the plugin's
[user guide](https://github.com/AgriciDaniel/banana-claude/blob/main/docs/guide.md)
for the richer plugin install (bundled MCP server and specialist agents),
which is not included in this standalone copy.

## n8n-MCP server

This repository also configures the [n8n-MCP](https://github.com/czlonkowski/n8n-mcp)
server (MIT License) at the project level via `.mcp.json`, so Claude Code
starts it automatically for anyone working in this project.

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "MCP_MODE": "stdio",
        "LOG_LEVEL": "error",
        "DISABLE_CONSOLE_OUTPUT": "true"
      }
    }
  }
}
```

As configured, this gives Claude access to n8n's bundled node/template
documentation and validation tools (no live n8n instance required). To let
Claude manage a real n8n instance (read executions, edit/validate/test
workflows, manage credentials), add to the `env` block in `.mcp.json`:

- `N8N_API_URL` — your n8n instance URL (e.g. `http://localhost:5678`)
- `N8N_API_KEY` — an API key from that instance

Since those are credentials, prefer setting them as a personal override
(`claude mcp add n8n-mcp --scope local ...`, or editing your own
`~/.claude.json`) rather than committing them into this shared `.mcp.json`.
See the [Claude Code setup guide](https://github.com/czlonkowski/n8n-mcp/blob/main/docs/CLAUDE_CODE_SETUP.md)
for details, scopes, and the optional companion
[n8n-skills](https://github.com/czlonkowski/n8n-skills) workflow-authoring skills.
