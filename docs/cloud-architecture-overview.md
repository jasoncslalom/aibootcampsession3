# Cloud Architecture Overview

This document provides a simple system context view for the TODO app monorepo.

## System Context

```mermaid
flowchart LR
    U[End User\nWeb Browser]

    subgraph MONO[Monorepo Deployment Context]
        FE[React Frontend\npackages/frontend]
        API[Express API\npackages/backend]
        DB[(In-Memory Data Store\nSQLite :memory:)]
    end

    U -->|HTTPS| FE
    FE -->|HTTP /api/tasks| API
    API -->|SQL queries| DB
```

## Notes

- The React frontend is the user-facing web application.
- The Express API exposes task endpoints used by the frontend.
- Data is stored in an in-memory SQLite database and resets when the backend process restarts.
- This is a simple logical system context and not a production cloud deployment topology.

## Sequence: User Creates a TODO

```mermaid
sequenceDiagram
    actor User
    participant Browser as Web Browser
    participant Frontend as React Frontend
    participant API as Express API
    participant Store as In-Memory SQLite

    User->>Browser: Enter title and submit TODO form
    Browser->>Frontend: Trigger form submit handler
    Frontend->>Frontend: Validate input (title required)

    Frontend->>API: POST /api/tasks { title, description, due_date }
    API->>API: Validate request payload
    API->>Store: INSERT task row
    Store-->>API: Return inserted row id
    API->>Store: SELECT created task by id
    Store-->>API: Return created task record
    API-->>Frontend: 201 Created + task JSON

    Frontend->>API: GET /api/tasks
    API->>Store: SELECT all tasks
    Store-->>API: Return task list
    API-->>Frontend: 200 OK + tasks JSON

    Frontend-->>Browser: Render updated task list with new TODO
    Browser-->>User: Show created TODO
```
