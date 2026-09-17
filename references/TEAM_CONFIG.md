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

- Trello: prefer direct file attachment when the available Composio tool supports it.
- Linear: use direct upload when supported; otherwise ask before placing the file in an approved shared store and attaching its access-controlled URL.
- Never upload evidence to Google Drive or another third party silently.

## Destination safety

If a configured name resolves to multiple targets, stop and ask the user to choose. If it resolves to none, report `Blocked by setup`. Do not create a replacement board, list, team, project, or label.
