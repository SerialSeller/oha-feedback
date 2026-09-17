# OHA Feedback Examples

## Two screenshots, two independent issues

Input:

> Screenshot 1: the back button looks too faint. Screenshot 2: Continue does nothing after I choose a team.

Output split:

1. Visual hierarchy issue for the back button. Map screenshot 1 as evidence; report it as not uploaded yet.
2. Functional Continue-button issue. Map screenshot 2 as evidence; report it as not uploaded yet.

Do not combine them merely because they came in one message.

## One screenshot, two visible problems

Input:

> In this screenshot the heading is cut off and the Save button is disabled even though every field is filled.

Output split:

1. Heading clipping issue, with the screenshot as evidence.
2. Save-button behavior issue, with the same screenshot as evidence because it visibly supports both claims.

## Multiple screenshots, one issue

Input:

> These three screenshots show the Cup name disappearing as I go back from Step 5.

Output split:

1. One data-persistence issue. Map all three screenshots in the order that demonstrates the flow, and report them as not uploaded yet.

## Missing context

Input:

> The layout moves off-screen here.

Use the visible screen name if it is legible. If device, OS, build, reproduction steps, PostHog replay, or Convex deploy are not provided, write `Not available`. Do not infer Android or iOS from the screenshot's appearance alone.

## Result response

```text
Issue 1 — Created
[UI] Back button has insufficient visual hierarchy
Trello: https://trello.com/c/...
Evidence: screenshot-1.png — not uploaded yet (current limitation)

Issue 2 — Blocked by setup
[Bug] Continue does not respond after team selection
Linear: the requested team is not visible in this Composio account
```

Report only states confirmed by the destination.
