# Managed OHA Intake Bridge

The managed bridge is the no-script path for teammates who send feedback from a phone or computer. A teammate installs this skill, attaches a screenshot, adds notes, and asks the AI client to create OHA feedback. The teammate does not run a local uploader, copy a file path, use Google Drive, or manually upload in Trello.

## What the bridge guarantees

- accepts only the actual bytes of PNG/JPG files;
- rejects local paths, URLs, mismatched image signatures, and suspiciously small files;
- stages bytes through the Composio Files API;
- passes `{name, mimetype, s3key}` to `TRELLO_ADD_CARDS_ATTACHMENTS_BY_ID_CARD`;
- maps each request to the requesting teammate's exact Composio Trello connected account;
- verifies filename, MIME type, exact byte size, Trello URL, and non-empty image previews;
- inserts the verified Trello attachment URL as a Markdown image directly below `Screenshot / clip`;
- retries only a failed attachment on the existing card and never recreates the card;
- never applies Trello labels.

## Current bridge endpoint

The current Cloudflare Worker endpoint is:

```text
https://oha-feedback-intake.muh-abdulkerim.workers.dev/mcp
```

The endpoint is not ready for teammates until the one-time owner setup below is complete. Do not put Composio keys, bridge tokens, or screenshots in this repository.

## One-time owner setup

The bridge owner completes this once. Teammates only connect their own Trello account and use the skill.

1. In Cloudflare Worker secrets, set `COMPOSIO_API_KEY` to the private Composio project key. Set `TRELLO_LIST_ID` to the verified `FEEDBACK & TESTING` list ID and set `OHA_USER_TOKENS_JSON` to a private mapping from one opaque bridge token to each teammate's own Composio Trello connected-account ID, such as `{ "private-token-for-alice": "ca_trello_alice" }`.
2. In the same Composio project, register the public MCP endpoint as a Custom MCP toolkit and sync its tools. Custom MCP is currently an experimental, API-only Composio feature; use its current official lifecycle rather than assuming the dashboard has a registration button.
3. Create the Custom MCP auth configuration with automatic account matching enabled. Each teammate must have an active Custom MCP connection containing their private bridge token, plus an active Trello connection in that same Composio project. Record only the Trello `ca_...` ID in the private Worker mapping.
4. Configure the approved AI clients to use the synced Custom MCP toolkit and this skill. A client must be able to forward the attached image's real bytes to `OHA_CREATE_FEEDBACK`. If it exposes only a filename or local path, the skill must stop as `Blocked by setup`.
5. Test on the approved existing test card only. Confirm in Trello that the image itself opens and previews, and record the attachment filename, MIME type, and exact byte size. Do not touch the eight existing live cards during the first test.

## Teammate flow

Attach one or more screenshots, write the notes, and invoke the skill. The skill drafts the canonical body, maps each screenshot to the right issue, checks for duplicates, and uses the bridge only after the normal approval rule is satisfied. Multiple screenshots may go to one card; independent issues must go to different cards. The bridge's successful result is not enough by itself—the skill must inspect the Trello card and return the verified card link.

## Transport boundary

MCP tool arguments are JSON, and not every AI client has a standard way to forward a conversation attachment into a tool call. The bridge includes a multipart `/intake` endpoint for clients that natively support authenticated multipart tool requests, but it is not a license to ask teammates to run scripts or upload to a third-party store. When the current client cannot provide real bytes, report `Blocked by setup` and leave Trello unchanged.

Official references:

- [Composio Files API](https://docs.composio.dev/reference/api-reference/files/postFilesUploadRequest)
- [Composio tool execution](https://docs.composio.dev/reference/api-reference/tools/postToolsExecuteByToolSlug)
- [Composio Custom MCP lifecycle](https://docs.composio.dev/docs/extending-sessions/custom-mcp)
- [Trello card attachments](https://developer.atlassian.com/cloud/trello/rest/api-group-cards/)
