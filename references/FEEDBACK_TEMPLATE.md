# OHA Feedback Template v1

Use this field order for every independent issue. Preserve the headings. Replace every bracketed instruction with factual content; if the information is absent, write `Not available`.

```text
What happened
[One factual line describing what went wrong.]

Where (screen / tab)
[For example: Match details, Create team, Profile.]

Steps to reproduce
1. [Observed or explicitly provided step.]
2. [Observed or explicitly provided step.]

Expected
[What should have happened.]

Screenshot / clip
[Direct attachment or approved shareable link.]

Context (auto-filled if reported in-app):
• App version: [value or Not available]
• Device / OS: [value or Not available]
• PostHog session replay: [value or Not available]
• Convex deploy: [value or Not available]
```

## Title

The destination title is outside the body template. Use:

```text
[Classification] Short observable problem in the affected area
```

Keep the title concise. State the symptom, not an unverified technical cause.

## Missing information

- Do not turn a screenshot into invented reproduction steps. Use `Not available` when actions are unknown.
- Do not combine device and OS guesses. Record only what the user or approved in-app context provides.
- Do not add `Actual`; `What happened` already serves that purpose.
- Do not add severity, owner, deadline, root cause, or implementation advice unless the team explicitly revises the canonical template.
