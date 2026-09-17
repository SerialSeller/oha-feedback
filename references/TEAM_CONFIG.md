# OHA Team Configuration

This file provides shared starting destinations. A teammate may override these in `USER_PREFERENCES.md` or specify a different accessible destination in chat.

## Trello

- Shared default: `yes`
- Workspace/board: `OOOHA! - WORKSPACE`
- List: `FEEDBACK & TESTING`
- Board ID: `RESOLVE THROUGH COMPOSIO`
- List ID: `RESOLVE THROUGH COMPOSIO`

Resolve the current IDs from the exact names before every write. Never fall back to the old copied boards named `Oha` or `Oha Test`.

## Linear

- Available: `yes — when the teammate connects Linear in Composio`
- Workspace/team: `CHOSEN BY THE TEAMMATE THROUGH COMPOSIO`
- Project: `CHOSEN BY THE TEAMMATE THROUGH COMPOSIO`
- Team ID: `RESOLVE THROUGH COMPOSIO`
- Project ID: `RESOLVE THROUGH COMPOSIO`

No single Linear workspace, team, or project is hardcoded. A teammate with access can choose the exact Linear destination they want, and the agent resolves it through that teammate's Composio connection before creating an issue.

## Evidence handling

- **Current limitation:** the shareable skill does not upload screenshot or clip files to Trello or Linear yet. The agent may analyze the files, but must report each one as `Not uploaded yet` after creating the destination item.
- Do not place evidence in Google Drive or another third party silently, and do not use a description filename, local path, thumbnail analysis, or linked cloud file as a substitute for a native attachment.
- When native upload support is restored, update this section with the verified Trello and Linear upload-and-readback flows before enabling attachment claims.

## Destination safety

If a requested name resolves to multiple targets, ask the teammate to choose. If it resolves to none, explain that the destination is not available through their connected account. Do not create a replacement board, list, team, or project unless the teammate explicitly asks for one.
