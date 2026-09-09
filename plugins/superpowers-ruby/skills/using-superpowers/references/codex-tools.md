# Codex Tool Mapping

Skills use Claude Code tool names. When you encounter these in a skill, use your platform equivalent:

| Skill references | Codex equivalent |
|-----------------|------------------|
| `Task` tool (dispatch subagent) | The host's current subagent/delegation tool (for example, `spawn_agent`; see [Named agent dispatch](#named-agent-dispatch)) |
| Multiple `Task` calls (parallel) | Multiple calls to the host's subagent/delegation tool |
| Task returns result | The host's current wait/collect mechanism (for example, `wait_agent`) |
| Task lifecycle | Follow the host's lifecycle controls; do not assume a separate cleanup command |
| `TodoWrite` (task tracking) | The host's current plan or task-tracking capability |
| `Skill` tool (invoke a skill) | Skills load natively — just follow the instructions |
| `Read`, `Write`, `Edit` (files) | Use your native file tools |
| `Bash` (run commands) | Use your native shell tools |

## Subagent dispatch

When subagents are available, dispatch each bounded task with the host's current
delegation capability (for example, `spawn_agent`), then use its current
wait/collect mechanism (for example, `wait_agent`) to retrieve results. Keep
progress in the host's plan or task-tracking capability. Availability and
configuration are host-specific, so do not assume fixed parameters or lifecycle
commands.

## Named agent dispatch

Claude Code skills reference named agent types like `superpowers-ruby:code-reviewer`.
Codex hosts may not expose a named-agent registry. Use the current delegation
tool (for example, `spawn_agent`) with a task name and prompt/message supported by
that host.

When a skill says to dispatch a named agent type:

1. Find the agent's prompt file (e.g., `agents/code-reviewer.md` or the skill's
   local prompt template like `code-quality-reviewer-prompt.md`)
2. Read the prompt content
3. Fill any template placeholders (`{BASE_SHA}`, `{WHAT_WAS_IMPLEMENTED}`, etc.)
4. Dispatch the task through the host's supported subagent interface, passing the
   filled prompt in its task input.

| Skill instruction | Codex equivalent |
|-------------------|------------------|
| `Task tool (superpowers-ruby:code-reviewer)` | Use the current delegation tool with the `code-reviewer.md` content as the task prompt |
| `Task tool (general-purpose)` with inline prompt | Use the current delegation tool with the same inline prompt |

### Message framing

The `message` parameter is user-level input, not a system prompt. Structure it
for maximum instruction adherence:

```
Your task is to perform the following. Follow the instructions below exactly.

<agent-instructions>
[filled prompt content from the agent's .md file]
</agent-instructions>

Execute this now. Output ONLY the structured response following the format
specified in the instructions above.
```

- Use task-delegation framing ("Your task is...") rather than persona framing ("You are...")
- Wrap instructions in XML tags — the model treats tagged blocks as authoritative
- End with an explicit execution directive to prevent summarization of the instructions

### When this workaround can be removed

This approach compensates for Codex's plugin system not yet supporting an
`agents` field in `plugin.json`. If a host later supports plugin-provided agents,
the package can expose them through that host's documented mechanism.

## Environment Detection

Skills that create worktrees or finish branches should detect their
environment with read-only git commands before proceeding:

```bash
GIT_DIR=$(cd "$(git rev-parse --git-dir)" 2>/dev/null && pwd -P)
GIT_COMMON=$(cd "$(git rev-parse --git-common-dir)" 2>/dev/null && pwd -P)
BRANCH=$(git branch --show-current)
```

- `GIT_DIR != GIT_COMMON` → already in a linked worktree (skip creation)
- `BRANCH` empty → detached HEAD (cannot branch/push/PR from sandbox)

See `using-git-worktrees` Step 0 and `finishing-a-development-branch`
Step 1 for how each skill uses these signals.

## Codex App Finishing

When the sandbox blocks branch/push operations (detached HEAD in an
externally managed worktree), the agent commits all work and informs
the user to use the App's native controls:

- **"Create branch"** — names the branch, then commit/push/PR via App UI
- **"Hand off to local"** — transfers work to the user's local checkout

The agent can still run tests, stage files, and output suggested branch
names, commit messages, and PR descriptions for the user to copy.
