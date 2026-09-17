# Client Adapters and Composio Setup

Canonical repository:

```text
https://github.com/SerialSeller/oha-feedback
```

Keep the folder intact. `SKILL.md` is the canonical entry point; the other files are loaded from `references/` when needed.

## Codex and ChatGPT desktop

For a personal install, copy the folder to:

```text
$HOME/.agents/skills/oha-feedback/
```

For a repository-scoped install, use:

```text
<repo>/.agents/skills/oha-feedback/
```

In Codex, ask `$skill-installer` to install the skill from `https://github.com/SerialSeller/oha-feedback`. Invoke it with `$oha-feedback` or ask naturally for OHA feedback handling. In ChatGPT desktop, select `@oha-feedback` when available. Restart the client only if it does not discover the new skill automatically.

For broader ChatGPT web/mobile team distribution, a maintainer can later package this skill and the Composio connector as a plugin. The standalone folder is intentionally the simpler v1.

## Claude Code and claude.ai

Claude Code personal install:

```text
~/.claude/skills/oha-feedback/
```

Claude Code project install:

```text
<project>/.claude/skills/oha-feedback/
```

Install from GitHub in Claude Code with:

```text
npx skills add https://github.com/SerialSeller/oha-feedback --skill oha-feedback
```

Invoke it as `/oha-feedback`, or ask naturally and let Claude activate it automatically. On claude.ai, upload a ZIP of the folder through the custom Skills area in Settings/Features when that account supports custom skills. Each user uploads their own copy; Claude surfaces do not automatically sync custom skills between one another.

## Gemini CLI

Use either user scope:

```text
~/.agents/skills/oha-feedback/
```

or workspace scope:

```text
<workspace>/.agents/skills/oha-feedback/
```

Install directly from GitHub with:

```text
gemini skills install https://github.com/SerialSeller/oha-feedback
```

During development, Gemini CLI can link the folder with `gemini skills link /absolute/path/to/oha-feedback`. Verify discovery with `/skills list` and refresh with `/skills reload`. Gemini normally activates the skill automatically when the request matches; `/oha-feedback` is not its portable invocation syntax.

## Other AI agents

If the agent supports the open Agent Skills folder format, install the whole folder in its documented skills directory. If it supports only persistent instructions, load `SKILL.md` as the main instruction and make every file under `references/` available alongside it. Do not paste only the workflow while omitting the template or team configuration.

## Connect Composio

Each teammate connects their own account and authorizes only the OHA Trello/Linear access they already have.

- Codex or Claude Code: Composio's native agent plugin/CLI path is the shortest setup when available.
- Any MCP-compatible client: connect Composio Connect at `https://connect.composio.dev/mcp`.
- Hosted clients: enable the authorized Composio app/plugin/connector offered by that client.

After connecting:

1. Confirm the account can see `OOOHA! - WORKSPACE` and `FEEDBACK & TESTING`.
2. List the board's exact existing labels.
3. Keep Linear disabled until the real OHA team is visible and recorded in `TEAM_CONFIG.md`.
4. Run a draft-only example before any external write.
5. Create a test card only with explicit approval, then verify its label, evidence, and returned URL.

Never place Composio keys, OAuth tokens, connected-account IDs, or personal credentials in this package.
