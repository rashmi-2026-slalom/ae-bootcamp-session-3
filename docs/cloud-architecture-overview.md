# Cloud Architecture Overview

This monorepo contains a browser-based React frontend, an Express API, and an in-memory data store used by the backend at runtime.

## System Context

```mermaid
flowchart LR
    User[User in Browser]
    Frontend[React Frontend<br/>packages/frontend]
    Api[Express API<br/>packages/backend]
    Store[(In-Memory SQLite Store)]

    User -->|Uses UI| Frontend
    Frontend -->|HTTP /api/tasks| Api
    Api -->|Reads and writes task data| Store
```

## Sequence: Create a TODO

```mermaid
sequenceDiagram
    actor User
    participant Frontend as React Frontend
    participant Api as Express API
    participant Store as In-Memory SQLite Store

    User->>Frontend: Enter task details and submit form
    Frontend->>Frontend: Validate required title
    Frontend->>Api: POST /api/tasks with task payload
    Api->>Api: Validate request body
    Api->>Store: Insert task record
    Store-->>Api: Return inserted task ID
    Api->>Store: Select newly created task
    Store-->>Api: Return created task
    Api-->>Frontend: 201 Created with task JSON
    Frontend->>Frontend: Refresh task list
    Frontend-->>User: Show new TODO in the UI
```

## Notes

- The frontend and backend live in the same npm workspace monorepo.
- The React frontend calls the Express API for task operations.
- The backend uses an in-memory SQLite database, so data is not persisted across server restarts.
