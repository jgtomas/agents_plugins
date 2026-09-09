# Superpowers Ruby

Superpowers Ruby is a self-contained, skills-only plugin for Ruby and Rails
development. It brings a composable planning, implementation, testing,
debugging, review, and delivery workflow to Codex and other Agent Plugins v1
hosts, with Ruby/Rails-specific guidance throughout.

This package vendors the upstream library at
[`99fac3d8bee27bab20b23d4bef6fa634738a59e8`](https://github.com/jgtomas/superpowers-ruby/commit/99fac3d8bee27bab20b23d4bef6fa634738a59e8)
(version 7.5.0). The pinned snapshot contains 35 skills and 191 supporting
files (226 files under `skills/` in total).

## Skills

The library is organized into four practical areas:

- **Workflow and collaboration:** `brainstorming`, `compound`,
  `compound-refresh`, `consulting-an-oracle`, `dispatching-parallel-agents`,
  `executing-plans`, `finishing-a-development-branch`, `handoff`,
  `handoff-list`, `handoff-resume`, `receiving-code-review`,
  `requesting-code-review`, `subagent-driven-development`,
  `using-git-worktrees`, `using-sqlite-worktrees`, `using-superpowers`,
  `verification-before-completion`, `writing-plans`, and `writing-skills`.
- **Ruby and Rails quality:** `37signals-style`, `brakeman`, `rails-guides`,
  `rails-upgrade`, `ruby`, `ruby-commit-message`, `ruby-upgrade`, and
  `sandi-metz-rules`.
- **Testing and debugging:** `test-driven-development` and
  `systematic-debugging`.
- **Hotwire:** `hwc-forms-validation`, `hwc-media-content`,
  `hwc-navigation-content`, `hwc-realtime-streaming`,
  `hwc-stimulus-fundamentals`, and `hwc-ux-feedback`.

The `skills/` directory is the portable discovery point. Each immediate child
contains an Agent Skills-compatible `SKILL.md`, with its references, examples,
and scripts kept beside it. The six upstream executable resources retain their
executable permissions.

## Installation

From this repository, register or refresh the marketplace and install the
plugin:

```bash
codex plugin marketplace add https://github.com/jgtomas/agents_plugins.git
codex plugin marketplace upgrade local-agent-plugins
codex plugin add superpowers-ruby@local-agent-plugins
```

Use `codex plugin marketplace upgrade local-agent-plugins` when the marketplace
is already registered and its snapshot needs refreshing. If you previously
registered this repository under its former marketplace identifier, re-register
or refresh it so Codex picks up `local-agent-plugins`. Start a new task after
installing or updating so the skill index is reloaded.

Example prompts:

- “Help me plan a Ruby or Rails feature.”
- “Audit this application before upgrading it to Ruby 4.”
- “Create a SQLite-backed git worktree with the current development data.”
- “Run `mode:autonomous` compound refresh for the Rails authentication area.”

## Packaging scope

This plugin intentionally contains only portable skills, the Superpowers Ruby
icon, both manifests, this documentation, and the upstream license. Hooks,
MCP integrations, commands, agents, platform installers, and upstream test
suites are excluded. Installing this skills-only package therefore does not
register lifecycle hooks or automatically create or move project files.

The portable Agent Plugins manifest is at [`plugin.json`](plugin.json); Codex UI
metadata is kept in [`.codex-plugin/plugin.json`](.codex-plugin/plugin.json).
The manifests use the `superpowers-ruby` namespace so upstream cross-skill
references continue to resolve.

## Attribution and license

This snapshot is maintained from
[`jgtomas/superpowers-ruby`](https://github.com/jgtomas/superpowers-ruby) and is
attributed to Lucian Ghinda. The vendored material retains Jesse Vincent’s
upstream MIT notice in [`LICENSE`](LICENSE).
