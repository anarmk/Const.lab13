# Architecture

## System overview

The app is a full-stack Next.js application. The frontend (React) and backend (API routes) live in the same project. Prisma talks to a local SQLite database file.

## Architecture diagram

```mermaid
graph TD
  subgraph Browser
    UI[React UI\nApp Router pages]
  end

  subgraph Next.js Server
    API[API Routes\n/api/tasks]
    MW[Middleware\nvalidation + error handling]
  end

  subgraph Data Layer
    PX[Prisma Client]
    DB[(SQLite\ndev.db)]
  end

  UI -->|fetch / HTTP| MW
  MW --> API
  API --> PX
  PX --> DB
```

## Layers

### 1. UI layer — `app/` (React components)
Next.js App Router pages and React components. Responsible for rendering the task list, forms, and filter bar. Communicates with the backend exclusively through `fetch()` calls to the API routes.

Key pages:
- `app/page.tsx` — main task dashboard
- `app/tasks/new/page.tsx` — create task form
- `app/tasks/[id]/edit/page.tsx` — edit task form

Key components:
- `components/TaskList.tsx` — renders the list of tasks
- `components/TaskCard.tsx` — individual task row with actions
- `components/TaskForm.tsx` — shared form for create and edit
- `components/FilterBar.tsx` — status and priority filters

### 2. API layer — `app/api/` (Next.js Route Handlers)
REST API endpoints that handle HTTP requests from the frontend. Each route validates the request, calls the Prisma service, and returns JSON.

| Method | Route | Action |
|--------|-------|--------|
| GET | `/api/tasks` | List all tasks (with filters) |
| POST | `/api/tasks` | Create a new task |
| GET | `/api/tasks/[id]` | Get a single task |
| PUT | `/api/tasks/[id]` | Update a task |
| DELETE | `/api/tasks/[id]` | Delete a task |

### 3. Data layer — `lib/` (Prisma + DB)
Prisma ORM manages all database access. The schema defines the Task model. All queries go through the Prisma Client — no raw SQL.

## Data model

```prisma
model Task {
  id          Int       @id @default(autoincrement())
  title       String
  description String?
  priority    Priority  @default(MEDIUM)
  status      Status    @default(ACTIVE)
  dueDate     DateTime?
  label       String?
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt
}

enum Priority {
  LOW
  MEDIUM
  HIGH
}

enum Status {
  ACTIVE
  COMPLETED
}
```

## Folder structure
const.lab13/
├── partB/
│   ├── src/
│   │   ├── app/
│   │   │   ├── page.tsx              # main dashboard
│   │   │   ├── layout.tsx
│   │   │   ├── tasks/
│   │   │   │   ├── new/page.tsx      # create form
│   │   │   │   └── [id]/edit/page.tsx
│   │   │   └── api/
│   │   │       └── tasks/
│   │   │           ├── route.ts      # GET all, POST
│   │   │           └── [id]/route.ts # GET one, PUT, DELETE
│   │   ├── components/
│   │   │   ├── TaskList.tsx
│   │   │   ├── TaskCard.tsx
│   │   │   ├── TaskForm.tsx
│   │   │   └── FilterBar.tsx
│   │   ├── lib/
│   │   │   ├── prisma.ts             # Prisma client singleton
│   │   │   └── validations.ts        # input validation helpers
│   │   └── types/
│   │       └── task.ts               # shared TypeScript types
│   ├── prisma/
│   │   ├── schema.prisma
│   │   └── dev.db
│   └── tests/

## Data flow example — creating a task

1. User fills out `TaskForm` and clicks "Save"
2. Component calls `fetch('/api/tasks', { method: 'POST', body: ... })`
3. `app/api/tasks/route.ts` receives the request, validates the body
4. Calls `prisma.task.create(...)`
5. Returns the new task as JSON
6. UI updates the task list with the new entry