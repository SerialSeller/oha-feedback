# OHA Feedback Skill

A portable Agent Skill for turning screenshots, clips, and short notes into consistent, actionable OHA feedback in Trello and Linear through Composio.

It gives Claude, Codex, Gemini, ChatGPT, and other compatible agents one shared feedback workflow while keeping client preferences editable for each teammate.

## What it does

- Splits independent problems into separate issues.
- Uses the official OHA Feedback Template v1.
- Maps the right evidence to the right issue. Native screenshot and clip upload is a known pending limitation; see [Evidence-upload limitation](#evidence-upload-limitation).
- Creates feedback without Trello labels.
- Creates only in verified OHA destinations enabled by the team.
- Uses `Not available` for missing context.
- Verifies the created destination and returns its Trello/Linear link with an honest evidence status.

## Workflow

```text
Screenshots + short notes
          ↓
Detect independent problems
          ↓
Build one structured report per problem
          ↓
Create in the teammate's chosen destination through Composio
          ↓
Return created links and clearly mark evidence as not uploaded yet
```

## Package layout

```text
oha-feedback/
├── SKILL.md                         Canonical workflow
├── README.md                        Setup and maintenance
├── agents/openai.yaml               Optional OpenAI/Codex metadata
└── references/
    ├── TEAM_CONFIG.md               Team-maintained destinations
    ├── FEEDBACK_TEMPLATE.md         Protected official template
    ├── USER_PREFERENCES.md          Per-teammate editable defaults
    ├── CLIENT_ADAPTERS.md           Claude/Codex/Gemini/ChatGPT notes
    └── EXAMPLES.md                  Splitting and evidence examples
```

## Start using it

1. Create a Composio account and connect the OHA **Trello** and/or **Linear** account you already use. Connect whichever destinations you want the skill to use.

2. Install the repository using the instructions in `references/CLIENT_ADAPTERS.md`:

   ```text
   https://github.com/SerialSeller/oha-feedback
   ```
3. Review `references/USER_PREFERENCES.md`. Teammates may change those preferences freely.
4. Ask the agent for a draft-only test:

   > Use the OHA Feedback skill. Draft feedback from these screenshots but do not create anything yet.

5. After the preview is correct, ask it to create the cards or issues in the destination you choose.

The shared starting destination is `OOOHA! - WORKSPACE` → `FEEDBACK & TESTING` in Trello. A teammate can instead choose another accessible Trello list, a Linear team/project, both destinations, or ask the agent to choose per report.

## Evidence-upload limitation

For now, screenshots and clips are input for the agent's analysis only. They are not uploaded to the Trello card or Linear issue, including as a link or embedded image in the description. The agent should create the structured feedback, return the card or issue link, and label the evidence result as **not uploaded yet**.

If native evidence must be available on a particular card today, attach it manually after the card is created. Do not treat a filename written in the description as an uploaded attachment.

## What teammates may customize

Teammates may edit `references/USER_PREFERENCES.md` or their own copy of the skill to choose:

- Trello only, Linear only, both, or a destination chosen per report.
- Their own default Trello board/list or Linear team/project.
- Preview first or immediate creation.
- Concise or detailed final responses.
- Their preferred default language.

They may also adapt installation notes, workflow wording, and the report template for their own workflow. The shared defaults keep issue splitting, evidence mapping, duplicate checks, and honest result reporting consistent; teammates can keep or adapt them in their own copy.

Do not commit API keys, OAuth tokens, connection IDs, private session links, or customer data into a shared copy of this package.

## Sharing and updates

Share the entire folder or its ZIP. Each teammate installs their own copy and connects their own Composio account. When distributing a new canonical version, preserve each teammate's `USER_PREFERENCES.md` or let them reapply those small choices.

Teammates can edit their installed copy. For a fix that should help everyone, fork the GitHub repository and open a pull request. Personal preferences belong in `references/USER_PREFERENCES.md`; changes to canonical rules, destinations, or the official template should be reviewed by the OHA team.

## Calling the skill

The skill is named `oha-feedback`, but invocation syntax belongs to the AI client:

- Claude Code: `/oha-feedback`
- Codex: `$oha-feedback`
- ChatGPT with installed skills: `@oha-feedback`
- Gemini CLI: ask naturally, such as `Turn these screenshots into OHA feedback`; Gemini activates matching skills automatically.

Explicit invocation is optional. The description is intentionally specific, so supported clients can automatically select the skill when a teammate asks to turn OHA screenshots, clips, or notes into feedback. Explicit invocation is useful when the agent does not select it or when the teammate wants certainty.

## Chat surfaces

- ChatGPT desktop supports standalone skills.
- ChatGPT web and mobile normal Chat/Work require the skill to be distributed inside an OpenAI plugin; a GitHub skill repository alone is not a one-click install there.
- Claude Code uses the repository-installed skill. Claude.ai supports custom skill ZIP uploads on eligible plans, not direct GitHub URL installation.
- Gemini CLI supports installation directly from the GitHub URL.

Before a team rollout, test one draft and one explicitly approved test card. Verify the board/list and returned link; the evidence result should explicitly say that upload is not available yet. Delete or archive the test card only through the team's normal process.

## Version

Package: `1.0.3`

Default team configuration:

- Trello: `OOOHA! - WORKSPACE` → `FEEDBACK & TESTING`
- Linear: available whenever the teammate connects and chooses an accessible Linear destination
