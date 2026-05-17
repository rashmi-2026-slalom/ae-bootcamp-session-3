# Functional Requirements for TODO App

This summary reflects the requirements discussion in the Sept. 16 meeting artifact and the Sept. 17 Slack confirmation.

## MVP Requirements

1. The app must support creating and editing tasks with a required `title`.
2. Each task may include an optional `dueDate` stored as an ISO `YYYY-MM-DD` value.
3. Invalid `dueDate` values must be ignored and treated as absent.
4. Each task must include a `priority` value of `P1`, `P2`, or `P3`.
5. New tasks must default to `priority: P3` when no priority is chosen.
6. Users must be able to mark tasks complete or incomplete.
7. Users must be able to view tasks in three filters: `All`, `Today`, and `Overdue`.
8. The `Today` and `Overdue` filters must show only incomplete tasks.
9. The `All` filter may show both complete and incomplete tasks.
10. Task data must remain local to the app, with no backend or external storage changes.

## Post-MVP Requirements

1. Overdue tasks should be visually highlighted so they stand out in the list.
2. Priority should be presented visually, such as with color-coded badges for `P1`, `P2`, and `P3`.
3. Tasks should be sorted in this order: overdue first, then priority (`P1` to `P3`), then due date ascending, with undated tasks last.

## Out of Scope

1. Notifications.
2. Recurring tasks.
3. Multi-user support.
4. Keyboard navigation and additional accessibility enhancements beyond the current baseline.
5. Backend persistence or other external storage.
