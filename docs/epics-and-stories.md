# Epics and Stories

Based on the requirements in `docs/prd-todo.md` and organized following the structure in `docs/templates/epic-and-stories-template.md`.

Technical requirements should reference the current implementation in `packages/frontend/src/App.js`, `packages/frontend/src/TaskForm.js`, `packages/frontend/src/TaskList.js`, and `packages/backend/src/app.js`.

## MVP

- Epic: Task Data Enhancements
  - Story: Add due date to tasks
    - Acceptance Criteria: Tasks support an optional due date field.
    - Technical Requirements: Extend the task payload passed from `TaskForm` through `App` save handlers to include due date values.
    - Technical Requirements: Preserve backend task records with a nullable `due_date` field in the current tasks table and API responses.
  - Story: Store due dates in ISO format
    - Acceptance Criteria: Due date values use the `YYYY-MM-DD` format.
    - Technical Requirements: Use the existing date input in `TaskForm` as the frontend entry point for `YYYY-MM-DD` values.
    - Technical Requirements: Keep the backend create and update endpoints aligned to accept and return due date values in `YYYY-MM-DD` form.
  - Story: Ignore invalid due date values
    - Acceptance Criteria: Invalid due date values are ignored.
    - Acceptance Criteria: Ignored invalid due date values are treated as absent.
    - Technical Requirements: Update frontend due date normalization and submission logic so invalid values are not persisted in outgoing task payloads.
    - Technical Requirements: Add backend validation in the current POST and PUT handlers so invalid due date values are stored as `null` rather than rejected or saved as-is.
  - Story: Add priority to tasks
    - Acceptance Criteria: Tasks support a priority value.
    - Acceptance Criteria: Allowed priority values are `P1`, `P2`, and `P3`.
    - Technical Requirements: Add priority state and input handling to `TaskForm` and include priority in the task payload sent by `App` save handlers.
    - Technical Requirements: Extend the backend task schema and create/update handlers to persist and return a `priority` field limited to `P1`, `P2`, or `P3`.
  - Story: Default new tasks to P3 priority
    - Acceptance Criteria: A task defaults to `P3` when no priority is selected.
    - Technical Requirements: Initialize new task form state in `TaskForm` with `P3` while preserving existing task values in edit mode.
    - Technical Requirements: Apply a backend default for `priority` when create requests omit the field.
  - Story: Require title for task creation and editing
    - Acceptance Criteria: Title is a required field.
    - Technical Requirements: Keep frontend submit validation in `TaskForm` for empty or whitespace-only titles.
    - Technical Requirements: Keep backend validation in POST and PUT handlers to reject empty task titles.

- Epic: Task Filtering
  - Story: Add All filter
    - Acceptance Criteria: The app provides an `All` filter.
    - Technical Requirements: Add filter selection state in `App` or `TaskList` and expose an `All` filter control in the task list UI.
    - Technical Requirements: Ensure the `All` filter requests or derives the complete task list without excluding completed items.
  - Story: Add Today filter
    - Acceptance Criteria: The app provides a `Today` filter.
    - Technical Requirements: Add a `Today` filter control to the current task list interface.
    - Technical Requirements: Implement filter logic against the due date field using the current task data returned by the backend.
  - Story: Add Overdue filter
    - Acceptance Criteria: The app provides an `Overdue` filter.
    - Technical Requirements: Add an `Overdue` filter control to the current task list interface.
    - Technical Requirements: Implement filter logic that compares due dates against the current date using the task data returned by the backend.
  - Story: Show completed tasks in All view
    - Acceptance Criteria: The `All` filter allows completed tasks to appear.
    - Acceptance Criteria: The `All` filter allows incomplete tasks to appear.
    - Technical Requirements: Keep `TaskList` rendering capable of showing both completed and incomplete tasks in the same result set.
    - Technical Requirements: Do not apply completion-based exclusion when the active filter is `All`.
  - Story: Hide completed tasks in Today view
    - Acceptance Criteria: The `Today` filter shows only incomplete tasks.
    - Technical Requirements: Exclude tasks with `completed` set to true when applying the `Today` filter.
    - Technical Requirements: Preserve the existing completion toggle behavior without surfacing completed tasks in `Today` results.
  - Story: Hide completed tasks in Overdue view
    - Acceptance Criteria: The `Overdue` filter shows only incomplete tasks.
    - Technical Requirements: Exclude tasks with `completed` set to true when applying the `Overdue` filter.
    - Technical Requirements: Preserve the existing completion toggle behavior without surfacing completed tasks in `Overdue` results.

- Epic: Local-Only Task Storage
  - Story: Keep task data stored locally
    - Acceptance Criteria: Task data remains stored locally.
    - Technical Requirements: Keep persistence within the current application runtime and local app experience rather than introducing remote storage.
    - Technical Requirements: Keep frontend task operations bound to the existing app stack instead of adding third-party storage integrations.
  - Story: Preserve no-backend task workflow
    - Acceptance Criteria: No backend changes are required for task storage.
    - Acceptance Criteria: No external storage changes are required.
    - Technical Requirements: Do not introduce new backend services, external databases, or third-party APIs for storage.
    - Technical Requirements: Limit backend changes to the current Express app and in-process data model needed to support the agreed task fields.

## Post-MVP

- Epic: Task Visual Indicators
  - Story: Highlight overdue tasks visually
    - Acceptance Criteria: Overdue tasks are visually highlighted.
    - Technical Requirements: Extend `TaskList` item styling to apply a distinct visual treatment when a task is overdue and incomplete.
    - Technical Requirements: Derive overdue status from the existing due date field during list rendering.
  - Story: Display color-coded priority badges
    - Acceptance Criteria: Priority is shown visually.
    - Acceptance Criteria: The visual priority treatment distinguishes `P1`, `P2`, and `P3`.
    - Technical Requirements: Add priority display elements to `TaskList` for tasks returned with a priority value.
    - Technical Requirements: Map `P1`, `P2`, and `P3` to distinct visual styles in the frontend component styling layer.

- Epic: Task Sorting
  - Story: Sort overdue tasks first
    - Acceptance Criteria: Overdue tasks appear before non-overdue tasks.
    - Technical Requirements: Update task ordering logic so overdue status is evaluated before other ordering rules.
    - Technical Requirements: Apply the overdue-first rule consistently to the task collection rendered by `TaskList`.
  - Story: Sort tasks by priority from P1 to P3
    - Acceptance Criteria: Tasks are ordered by priority from `P1` to `P3`.
    - Technical Requirements: Add priority rank ordering to the current task sorting pipeline.
    - Technical Requirements: Ensure priority sorting operates on the persisted `priority` values returned by the backend.
  - Story: Sort tasks by due date ascending
    - Acceptance Criteria: Tasks are ordered by due date in ascending order.
    - Technical Requirements: Preserve due date ordering as an explicit step in the task sort sequence.
    - Technical Requirements: Apply ascending comparisons only to tasks with valid due date values.
  - Story: Place undated tasks last
    - Acceptance Criteria: Tasks without a due date appear after dated tasks.
    - Technical Requirements: Keep tasks with missing due dates at the end of the sorted collection.
    - Technical Requirements: Ensure null or absent due date values are handled explicitly in sorting logic rather than relying on implicit comparison behavior.
