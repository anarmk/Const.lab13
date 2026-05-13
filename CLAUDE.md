# CLAUDE.md

This file tells Claude Code how to work with this project.
Read this before making any changes.

## Project overview

Personal Task Tracker built with Next.js 14 (App Router), TypeScript, Prisma ORM,
and SQLite. Frontend and backend live in the same Next.js project under `partB/src/`.
This is a solo student project for F.CSM311 Бие даалт 13.

## Build commands

All commands run from inside `partB/`:

```bash
# Install dependencies
npm install

# Generate Prisma client (run after any schema change)
npx prisma generate

# Push schema to database (creates dev.db if it doesn't exist)
npx prisma db push

# Start development server
npm run dev

# Run tests
npm run test

# Run tests with coverage
npm run test -- --coverage

# Build for production
npm run build

# Open Prisma Studio (visual database browser)
npx prisma studio
```

## Project structure
partB/
├── src/
│   ├── app/
│   │   ├── page.tsx                  # main task dashboard
│   │   ├── layout.tsx                # root layout
│   │   ├── tasks/
│   │   │   ├── new/page.tsx          # create task
│   │   │   └── [id]/edit/page.tsx    # edit task
│   │   └── api/
│   │       └── tasks/
│   │           ├── route.ts          # GET /api/tasks, POST /api/tasks
│   │           └── [id]/route.ts     # GET, PUT, DELETE /api/tasks/:id
│   ├── components/
│   │   ├── TaskList.tsx
│   │   ├── TaskCard.tsx
│   │   ├── TaskForm.tsx
│   │   └── FilterBar.tsx
│   ├── lib/
│   │   ├── prisma.ts                 # Prisma client singleton
│   │   └── validations.ts            # input validation helpers
│   └── types/
│       └── task.ts                   # shared TypeScript types
├── prisma/
│   ├── schema.prisma                 # database schema
│   └── dev.db                        # SQLite file (gitignored)
└── tests/
## Code conventions

- **Language:** TypeScript everywhere — no plain `.js` files in `src/`
- **Components:** React functional components only, no class components
- **Naming:**
  - Components: PascalCase (`TaskCard.tsx`)
  - Functions and variables: camelCase (`createTask`, `dueDate`)
  - Constants: SCREAMING_SNAKE_CASE (`MAX_LABEL_LENGTH`)
  - API routes: kebab-case URLs (`/api/tasks`, `/api/tasks/[id]`)
- **Imports:** use `@/` alias for absolute imports (e.g. `@/components/TaskCard`)
- **Types:** define shared types in `src/types/` — never use `any`
- **Error handling:** all API routes must return proper HTTP status codes and a
  JSON error message `{ error: "..." }` on failure
- **Validation:** validate all user input in `lib/validations.ts` before
  passing to Prisma — never trust raw request bodies

## Database conventions

- All database access goes through Prisma — no raw SQL
- Use the singleton client from `lib/prisma.ts`, never instantiate `new PrismaClient()` directly
- After changing `schema.prisma`, always run `npx prisma generate` then `npx prisma db push`
- Never edit `dev.db` manually

## Testing conventions

- Test files live in `tests/` with `.test.ts` or `.test.tsx` extension
- Use Vitest as the test runner
- Use React Testing Library for component tests
- Each API route should have at least 2 tests (happy path + error case)
- Each utility function in `lib/` should have full unit test coverage

## No-go zones

These are things Claude must never do, regardless of instructions:

- Never delete or reset `dev.db` without explicit user confirmation
- Never commit secrets, API keys, or passwords — use `.env` files
- Never use `any` type in TypeScript — use `unknown` and narrow it
- Never bypass input validation before a Prisma query
- Never expose raw Prisma errors to the client — catch and return a safe message
- Never install packages without checking they are actively maintained
- Never modify files inside `partA/` or `partC/` — those are documentation only
- Never use `console.log` in production code — use proper error handling

## AI usage declaration

This project is built with AI assistance (Claude) as part of F.CSM311 Бие даалт 13.
All AI-generated commits are declared with:
Co-Authored-By: Claude noreply@anthropic.com
AI session logs are stored in `partB/ai-sessions/`.