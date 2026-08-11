# Rollbar Triage Codex Plugin

This package contains one Codex plugin with three skills:

- `rollbar-analyzer`
- `rollbar-classifier`
- `rollbar-urgency-assessor`

The plugin uses Rollbar's MCP server via `npx -y @rollbar/mcp-server@latest`.

## Requirements

- Codex with plugin support
- Node.js 20 or 22
- `npx`
- A Rollbar read-scope access token

## 1. Configure Rollbar authentication

For one Rollbar project, export the access token before launching Codex:

```bash
export ROLLBAR_ACCESS_TOKEN='YOUR_ROLLBAR_READ_TOKEN'
```

Do not commit your real token to this plugin directory.

Alternatively, create `~/.rollbar-mcp.json` for one or multiple projects.

Single project:

```json
{ "token": "YOUR_ROLLBAR_READ_TOKEN" }
```

Multiple projects:

```json
{
  "projects": [
    { "name": "backend", "token": "TOKEN_1" },
    { "name": "frontend", "token": "TOKEN_2" }
  ]
}
```

## 2. Install as a local Codex marketplace

From the directory that contains this README:

```bash
codex plugin marketplace add "$(pwd)"
codex plugin list
```

Then install the plugin using the marketplace name:

```bash
codex plugin add rollbar-triage@local-rollbar-plugins
```

Start a new Codex thread/session after installation so the skills and MCP tools are loaded.

## 3. Try it

Examples:

```text
Analyze Rollbar item 123456.
```

```text
Classify Rollbar item 123456.
```

```text
Assess the urgency of Rollbar item 123456.
```

Codex should select the corresponding skill and use the Rollbar MCP tools.

## Structure

```text
.
├── .agents/
│   └── plugins/
│       └── marketplace.json
└── plugins/
    └── rollbar-triage/
        ├── .codex-plugin/
        │   └── plugin.json
        ├── .mcp.json
        └── skills/
            ├── rollbar-analyzer/
            │   └── SKILL.md
            ├── rollbar-classifier/
            │   └── SKILL.md
            └── rollbar-urgency-assessor/
                └── SKILL.md
```
