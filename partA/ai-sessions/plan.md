# AI planning session — Part A

- **Date:** 2026-05-13
- **Goal:** Choose a project topic, select a tech stack, and define the architecture
  before writing any code.
- **Tool:** Claude (claude.ai)

---

## Session summary

### Exchange 1 — Understanding the assignment

**Student:** Let's do this [uploaded assignment PDF]

**Claude:** Summarized the 3-part structure (Plan / Build / Reflect), identified
the key deliverables for each section, and built an interactive dashboard to
navigate the assignment requirements.

---

### Exchange 2 — Choosing a project topic

**Student:** Give me an overview on each option.

**Claude:** Described all 4 topic options:
- URL Shortener — simplest scope, API-focused
- Personal Task Tracker — classic CRUD with filters, moderate UI
- Markdown Notes — most interesting features, PDF export challenge
- Mini Library — best data modeling, 3 related entities

Recommended URL Shortener for easiest pass, Mini Library or Markdown Notes
for more impressive output.

**Decision:** Personal Task Tracker chosen by student.

---

### Exchange 3 — Stack comparison

**Student:** Give me three options on tech stack and discuss pros and cons.

**Claude:** Presented three options:

1. Node.js + Express + SQLite — simple, no TypeScript, no frontend included
2. Python + FastAPI + SQLite — auto OpenAPI docs, no frontend included
3. Next.js + TypeScript + Prisma + SQLite — full-stack, steepest learning curve

Key insight discussed: Options 1 and 2 require managing two separate projects
(API + React frontend). Option 3 unifies them in one repo.

**Decision:** Next.js + TypeScript + Prisma + SQLite chosen.

---

### Exchange 4 — Scoping the UI

**Student:** I want UI, I know the basics on React but want to learn, this is
my first time with Next.js.

**Claude:** Recommended keeping scope realistic for a first Next.js project:
- Include a full React frontend using App Router
- No authentication (single user, no login)
- No PDF export
- 4-5 solid features rather than many half-finished ones

Features agreed on:
1. Task list dashboard
2. Create / edit task form
3. Priority levels (Low / Medium / High)
4. Due dates and labels
5. Filter by status and priority
6. Mark complete / incomplete

---

### Exchange 5 — Part A documents generated

Documents produced in sequence with student review at each step:

| File | Key decisions captured |
|------|----------------------|
| `PROJECT.md` | Scope defined, out-of-scope items listed explicitly |
| `ARCHITECTURE.md` | Mermaid diagram, Prisma schema, folder structure, data flow |
| `STACK-COMPARISON.md` | 3 stacks compared across 6 criteria, decision justified |
| `CLAUDE.md` | Build commands, conventions, no-go zones documented |
| `ADR-001` | Formal record of stack decision with rationale and consequences |

---

## Key decisions made

1. **Project:** Personal Task Tracker (not URL Shortener or Mini Library)
2. **Stack:** Next.js 14 + TypeScript + Prisma + SQLite + Tailwind + Vitest
3. **Scope:** UI included, no auth, no PDF export, 5 core features
4. **Structure:** Single Next.js project for both frontend and backend
5. **No-go zones:** Defined in CLAUDE.md — no raw SQL, no `any` type, no secrets in code

## What Claude got right

- Correctly identified that splitting frontend/backend into two projects adds
  unnecessary complexity for a 2-week solo assignment
- Mermaid diagram and Prisma schema produced cleanly with no corrections needed
- CLAUDE.md no-go zones were comprehensive and required no additions

## What to watch for in Part B

- App Router server vs client component confusion — Claude flagged this as a
  likely sticking point for a first Next.js project
- Remember to run `npx prisma generate` after any schema change
- Start commits on day 1 — the ≥15 commits across ≥5 days requirement means
  there is no room to rush at the end