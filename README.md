# Agent Plugins

This repository contains portable Agent Plugins and their Codex marketplace
metadata.

## Plugins

- [Rollbar Triage](plugins/rollbar-triage/README.md) — analyze, classify, and prioritize Rollbar errors.

## Install from GitHub

After cloning or pushing this repository, register the repository as a Codex
marketplace and install the plugin:

```bash
codex plugin marketplace add https://github.com/jgtomas/agents_plugins.git
codex plugin add rollbar-triage@local-rollbar-plugins
```

For local development from this checkout:

```bash
codex plugin marketplace add "$(pwd)"
codex plugin add rollbar-triage@local-rollbar-plugins
```

Start a new Codex thread after installation so updated skills and MCP tools are
loaded.

## Repository layout

```text
.
├── .agents/plugins/marketplace.json
└── plugins/
    └── rollbar-triage/
```

See the [Agent Plugins specification](https://agent-plugins.org/specification)
for the portable package format.
