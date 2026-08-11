# Rollbar Triage

Rollbar Triage is an Agent Plugin for investigating Rollbar errors. It uses
Rollbar's MCP server and provides three focused skills:

- `rollbar-analyzer` — investigate an error, correlate it with deployments and related failures, and recommend remediation.
- `rollbar-classifier` — classify an error as a third-party API issue, in-house API issue, bug, or noise, with evidence and confidence.
- `rollbar-urgency-assessor` — assess urgency as HIGH, MEDIUM, or LOW and determine notification timing from impact and frequency.

## MCP server

The plugin launches Rollbar's MCP server through:

```text
npx -y @rollbar/mcp-server@latest
```

The portable configuration is in [`mcp.json`](mcp.json). The Codex adapter
configuration is in [`.mcp.json`](.mcp.json).

## Authentication

Agent Plugins does not define a portable credential-reference field. Configure
Rollbar authentication using the mechanism supported by your client. For the
Codex/Rollbar MCP server, use a read-scope token before starting Codex.

For one Rollbar project:

```bash
export ROLLBAR_ACCESS_TOKEN='YOUR_ROLLBAR_READ_TOKEN'
```

Alternatively, create `~/.rollbar-mcp.json`:

```json
{ "token": "YOUR_ROLLBAR_READ_TOKEN" }
```

For multiple projects:

```json
{
  "projects": [
    { "name": "backend", "token": "TOKEN_1" },
    { "name": "frontend", "token": "TOKEN_2" }
  ]
}
```

Never commit a real access token to this repository.

## Usage

Once installed, ask Codex for example:

```text
Analyze Rollbar item 123456.
```

```text
Classify Rollbar item 123456.
```

```text
Assess the urgency of Rollbar item 123456.
```

The plugin root contains both the portable Agent Plugins files and the
Codex-specific adapter files:

```text
rollbar-triage/
├── plugin.json
├── mcp.json
├── .codex-plugin/plugin.json
├── .mcp.json
└── skills/
```

See the [Agent Plugins specification](https://agent-plugins.org/specification)
and [Agent Skills specification](https://agentskills.io/specification) for the
portable format requirements.
