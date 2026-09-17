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
2. Keep Linear disabled until the real OHA team is visible and recorded in `TEAM_CONFIG.md`.
3. Run a draft-only example before any external write.
4. Create a test card only with explicit approval, then verify its native file attachment and returned URL.

### No-script shared bridge

For teammates using phones, desktops, or hosted AI clients, the recommended shared path is the managed OHA intake bridge described in [INTAKE_BRIDGE.md](INTAKE_BRIDGE.md). It is a remote service behind this skill, not a script teammates install or run. The maintainer configures it once with Cloudflare Worker secrets and Composio Custom MCP; every teammate then uses their own Composio/Trello connection.

The bridge must receive actual image bytes. An AI client that forwards only `/Users/.../screenshot.png`, a filename, or a URL is not compatible with native evidence upload. Report `Blocked by setup` for that client instead of trying the Trello action. Never ask a teammate to encode a screenshot manually.

When executing uploads through a Composio SDK, inspect the current Trello tool
schema first. Automatic handling is valid only if the attachment field is
explicitly marked `file_uploadable`. Then enable automatic file handling,
keep sensitive-file protection enabled, and allowlist the approved evidence
directory. Pass the local PNG/JPG path only to that SDK call; never pass it as
plain text to a hosted MCP action.

If the client exposes Composio Tool Router session files, upload the screenshot
to the current session first and pass the fresh staged file reference to the
Trello action. If neither direct SDK upload nor session-file upload is
available, report `Blocked by setup`. Do not substitute a URL or cloud store.

Never place Composio keys, OAuth tokens, connected-account IDs, or personal credentials in this package.

### Native Trello screenshot uploads

Use `TRELLO_ADD_CARDS_ATTACHMENTS_BY_ID_CARD` only after the file transport is
proven. The action must receive either a SDK-produced FileUploadable reference
or a fresh Composio session-file reference in `file`; it must not receive a
Mac/local path as text and must not receive `url` for local evidence.

### Put the screenshot inside the description

Trello's supported editor behavior is "attach and insert link": the image is
stored as a native card attachment and a reference to that attachment is
inserted in the description. Reproduce this through Composio sequentially:

1. Attach the real PNG/JPG and verify its filename, MIME type, byte size, and
   image preview.
2. Read the attachment and obtain its Trello `url`.
3. Update the full card description, replacing the `Screenshot / clip` line
   with `![filename](trello-attachment-url)` immediately below it.
4. Read the card again and verify that the saved description contains the
   Trello attachment URL and that the attachment still has a preview.

Never put a local path, Composio `s3key`, presigned staging URL, or a filename
alone in the description. Never delete the attachment after embedding it.

After execution, read the card's attachments and require the expected filename,
`image/png` or `image/jpeg`, a non-trivial byte count matching the source, and
an actual Trello image preview. If execution is uncertain, verify first and
retry only that attachment against the same existing card. Never recreate the
card. Keep credentials and screenshots outside the shared skill repository.
