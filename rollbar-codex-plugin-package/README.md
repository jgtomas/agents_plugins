# Rollbar Triage Agent Plugin

This package contains one portable Agent Plugin with three skills:

- `rollbar-analyzer`
- `rollbar-classifier`
- `rollbar-urgency-assessor`

The portable plugin uses Rollbar's MCP server via `npx -y @rollbar/mcp-server@latest`.
The root `plugin.json` and `mcp.json` files follow the Agent Plugins 1.0.0
format. The `.codex-plugin/` and `.mcp.json` files are retained as Codex
marketplace adapter metadata.

## Requirements

- An Agent Plugins-compatible client
- Codex with plugin support (for the local marketplace workflow below)
- Node.js 20 or 22
- `npx`
- A Rollbar read-scope access token

## Configure Rollbar authentication

Agent Plugins does not define a portable credential-reference field. Configure
Rollbar authentication using the mechanism supported by your client. For the
Codex/Rollbar MCP server, use one of the following before starting Codex:

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

## Install as a local Codex marketplace

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

## Try it

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

## Portable package structure

```text
plugins/
└── rollbar-triage/
    ├── plugin.json
    ├── mcp.json
    └── skills/
        ├── rollbar-analyzer/
        │   └── SKILL.md
        ├── rollbar-classifier/
        │   └── SKILL.md
        └── rollbar-urgency-assessor/
            └── SKILL.md
```

The repository also contains `.agents/plugins/marketplace.json` and the
Codex-specific adapter files used by the local Codex marketplace workflow.

See the [Agent Plugins specification](https://agent-plugins.org/specification)
and [Agent Skills specification](https://agentskills.io/specification) for the
portable format requirements.
