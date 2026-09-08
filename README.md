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
