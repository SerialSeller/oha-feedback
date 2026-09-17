# OHA Label Rules

Classify from observed user-facing behavior, then attach an exact label that already exists on the configured Trello board.

## Semantic mapping

| Observed problem | Preferred label family |
|---|---|
| A control fails, data is lost, a request errors, or behavior is functionally broken | `Bug` or `Development` |
| Spacing, alignment, hierarchy, color, typography, or visual inconsistency | `UI` or `Design / UX` |
| A flow is confusing, hard to discover, or behaves contrary to user expectations | `UX` or `Design / UX` |
| Wording, translation, grammar, or content is wrong | `Content` or the board's equivalent content label |
| Slowness, freezing, excessive loading, or responsiveness problems | `Performance` or `Development` |
| Contrast, focus, screen-reader, text-size, or touch-target barriers | `Accessibility` or `Design / UX` |

These are semantic families, not permission to create labels with those names.

## Resolve the exact board label

1. List labels on `OOOHA! - WORKSPACE` through the authorized Trello connection.
2. Match the issue to the narrowest exact existing label.
3. If both a broad and narrow label clearly apply, follow the teammate preference for one or multiple labels.
4. If no exact match exists, or two labels are equally plausible, ask the user. Do not invent, rename, or create a label.
5. Record the exact chosen label in the preview and verify it appears on the created card.

## Classification rules

- Classify the symptom, not a guessed root cause.
- A visual defect and a broken action in the same screenshot are separate issues when they need separate fixes.
- Pure UX feedback is not automatically a bug.
- `Unknown` is acceptable in the preview when evidence is insufficient; ask before creating if an exact label is required.
