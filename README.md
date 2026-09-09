# Agent Plugins

This repository contains portable Agent Plugins and their Codex marketplace
metadata.

## Plugins

- [Rollbar Triage](plugins/rollbar-triage/README.md) — analyze, classify, and prioritize Rollbar errors.
- [Superpowers Ruby](plugins/superpowers-ruby/README.md) — Ruby/Rails planning, implementation, testing, debugging, and review workflows.

## Install from GitHub

After cloning or pushing this repository, register the repository as a Codex
marketplace and install the plugin:

```bash
codex plugin marketplace add https://github.com/jgtomas/agents_plugins.git
codex plugin add rollbar-triage@local-agent-plugins
codex plugin add superpowers-ruby@local-agent-plugins
```

If the marketplace is already registered, refresh its snapshot before
installing an updated plugin:

```bash
codex plugin marketplace upgrade local-agent-plugins
codex plugin add superpowers-ruby@local-agent-plugins
```

If you previously registered this repository under its former marketplace
identifier, re-register or refresh it so Codex picks up `local-agent-plugins`
before installing plugins.

For local development from this checkout:

```bash
codex plugin marketplace add "$(pwd)"
codex plugin add rollbar-triage@local-agent-plugins
codex plugin add superpowers-ruby@local-agent-plugins
```

Start a new Codex task after installing or updating so the plugin's skills are
loaded.

## Repository layout

```text
.
├── .agents/plugins/marketplace.json
└── plugins/
    ├── rollbar-triage/
    └── superpowers-ruby/
```

See the [Agent Plugins specification](https://agent-plugins.org/specification)
for the portable package format.
