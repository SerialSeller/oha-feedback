# OHA Team Configuration

This file contains shared destinations, not personal preferences. A team maintainer may edit it only after verifying the current names and IDs through the connected OHA accounts.

## Trello

- Enabled: `yes`
- Workspace/board: `OOOHA! - WORKSPACE`
- List: `FEEDBACK & TESTING`
- Board ID: `RESOLVE THROUGH COMPOSIO`
- List ID: `RESOLVE THROUGH COMPOSIO`

Resolve the current IDs from the exact names before every write. Never fall back to the old copied boards named `Oha` or `Oha Test`.

## Linear

- Enabled: `no`
- Workspace/team: `NOT CONFIGURED`
- Project: `NOT CONFIGURED`
- Team ID: `NOT CONFIGURED`
- Project ID: `NOT CONFIGURED`

`Oha test` was used only for an earlier integration test. It is not the production OHA destination. Enable Linear only after the teammate can see the real OHA team and a maintainer records the verified destination here.

## Evidence handling

- Evidence attachment is required for every screenshot or clip mapped to an issue.
- Trello: upload the local file with the attachment operation, then read the card's attachment list and verify the filename is present.
- Linear: use the prepare-upload → raw-byte upload → create-attachment sequence, then read the issue and verify the attachment is present.
- If direct upload is unavailable, ask before placing the file in an approved shared store and attaching its access-controlled URL.
- Never upload evidence to Google Drive or another third party silently.
- Never treat a filename written in the description as a successful attachment.

## Destination safety

If a configured name resolves to multiple targets, stop and ask the user to choose. If it resolves to none, report `Blocked by setup`. Do not create a replacement board, list, team, project, or label.
