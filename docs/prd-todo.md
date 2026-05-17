# Product Requirements Document (PRD) - TODO App Upgrade

## 1. Overview

We are upgrading the current basic TODO app to make it more useful without overcomplicating it. Based on the Sept. 16 requirements meeting and the Sept. 17 Slack confirmation, the product direction for this phase is a simple, teachable MVP with no backend changes. The confirmed MVP adds due dates, task priority, and date-based filters while keeping storage local to the app. Visual overdue treatment and advanced sorting were explicitly deferred to post-MVP.

---

## 2. MVP Scope

- Add an optional `dueDate` field to each task.
- Store `dueDate` as an ISO `YYYY-MM-DD` value.
- Ignore invalid `dueDate` values and treat them as absent.
- Add a `priority` field with allowed values `P1`, `P2`, and `P3`.
- Default `priority` to `P3` when no priority is selected.
- Treat `title` as a required field.
- Provide task filters for `All`, `Today`, and `Overdue`.
- In `All`, allow both completed and incomplete tasks to appear.
- In `Today`, show only incomplete tasks.
- In `Overdue`, show only incomplete tasks.
- Keep storage local only.
- Do not make backend or external storage changes.

---

## 3. Post-MVP Scope

- Visually highlight overdue tasks so they stand out.
- Show priority visually, such as with color-coded badges for `P1`, `P2`, and `P3`.
- Sort tasks in this order: overdue first, then priority from `P1` to `P3`, then due date ascending, with undated tasks last.

---

## 4. Out of Scope

- Notifications.
- Recurring tasks.
- Multi-user support.
- Keyboard navigation.
- External storage.
