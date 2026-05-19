# ADR-001 — Stack selection

- **Status:** Accepted
- **Date:** 2026-05-13
- **Author:** Student + Claude (AI assistant)

## Context

For F.CSM311 Бие даалт 13 we need to build a small but complete software system
with a minimum of 3 working features, a test suite, and a real development workflow.
The project chosen is a Personal Task Tracker with a UI.

The stack decision had to satisfy these constraints:

- Solo developer, 2-week deadline
- Must include a working frontend UI (not just an API)
- Must support at least 10 unit tests
- Must be realistic enough to generate meaningful AI session logs
- Developer has basic React knowledge but no prior Next.js experience
- Developer is comfortable learning new tools with AI assistance

Three stacks were evaluated. Full comparison is in `partA/STACK-COMPARISON.md`.

## Decision

**Use Next.js 14 (App Router) + TypeScript + Prisma ORM + SQLite + Tailwind CSS + Vitest**

## Alternatives considered

### Option A — Node.js + Express + SQLite
Rejected because it does not include a frontend. Managing two separate projects
(an Express API and a React app) within a 2-week solo assignment adds unnecessary
overhead. Also lacks TypeScript by default, which increases the risk of runtime bugs.

### Option B — Python + FastAPI + SQLite
Rejected for the same frontend reason — FastAPI is an API-only framework. The
auto-generated OpenAPI docs are a genuine advantage, but the cost of running and
coordinating two separate projects outweighs it. Also, the student is more
comfortable with JavaScript/TypeScript than Python.

## Rationale for chosen stack

**Next.js** was chosen because it unifies frontend and backend in a single project.
One `npm run dev` command runs everything. The App Router (introduced in Next.js 13)
is the current recommended approach and worth learning properly.

**TypeScript** was chosen over plain JavaScript because type errors are caught at
compile time rather than at runtime. For a beginner working with AI-generated code,
TypeScript acts as a second reviewer — it will reject code that looks plausible but
uses the wrong shape of data.

**Prisma** was chosen over raw SQL or other ORMs because its schema file is
human-readable, the generated client is fully typed, and it handles migrations
automatically with `prisma db push`. This removes an entire category of database
bugs without requiring deep SQL knowledge.

**SQLite** was chosen over PostgreSQL or MySQL because it requires zero server
setup — the database is a single file (`dev.db`). For a local solo project with
no concurrent users this is the right tradeoff.

**Tailwind CSS** was chosen for styling because it works naturally with Next.js,
requires no separate CSS files, and is fast to iterate with.

**Vitest** was chosen for testing because it is the recommended test runner for
Vite-based projects, has a Jest-compatible API, and runs significantly faster than
Jest for TypeScript projects.

## Consequences

### Positive
- Single repo, single dev server, single deployment unit
- TypeScript catches mistakes before runtime
- Prisma schema serves as living documentation of the data model
- App Router knowledge is directly transferable to real industry projects
- Strong ecosystem — excellent documentation, large community

### Negative
- App Router introduces the concept of server vs client components which
  can be confusing for beginners (e.g. `"use client"` directive)
- Prisma adds a generation step — forgetting `npx prisma generate` after
  schema changes causes confusing errors
- Next.js is a larger framework than needed for a simple task tracker —
  some complexity exists purely because of the framework, not the problem

### Mitigations
- CLAUDE.md documents the build commands clearly to avoid the Prisma pitfall
- The no-go zones in CLAUDE.md prevent the most common beginner mistakes
- AI assistant (Claude) is available to explain server vs client component
  confusion as it comes up during development