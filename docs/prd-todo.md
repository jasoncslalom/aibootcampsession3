# Product Requirements Document (PRD) - Todo App Upgrade (MVP and Post-MVP)

## 1. Overview

The current Todo app is intentionally basic and only supports a task title and completion status. This upgrade improves usefulness while keeping implementation lean and teachable.

The product direction is to add lightweight planning capabilities for individual users through due dates, priority levels, and date-based filtering, while keeping all data local and avoiding backend changes. Scope is explicitly split into MVP, Post-MVP, and Out of Scope to protect delivery simplicity.

---

## 2. MVP Scope

- Add dueDate to each task as an optional field.
- dueDate format must be ISO date string: YYYY-MM-DD.
- Add priority to each task with enum values: P1, P2, P3.
- Default priority to P3 when not provided.
- Add task filters with three views: All, Today, Overdue.
- Keep storage local only; do not introduce backend or external storage.
- Preserve simple MVP behavior suitable for teaching and incremental implementation.

MVP data model and validation:
- title is required.
- priority must be one of P1, P2, P3; default is P3.
- dueDate is optional.
- Invalid dueDate values are ignored and treated as absent.

---

## 3. Post-MVP Scope

- Add visual highlighting for overdue tasks.
- Add task sorting with the following order:
- overdue tasks first
- then priority order (P1 to P3)
- then dueDate ascending
- tasks without dueDate last

---

## 4. Out of Scope

- Notifications
- Recurring tasks
- Multi-user support
- Keyboard navigation enhancements
- External storage integrations
- Backend changes
