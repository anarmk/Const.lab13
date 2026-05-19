# Stack comparison

## Candidates evaluated

Three stacks were compared before starting the project. All three are capable of
building a personal task tracker, but they differ in complexity, learning curve,
and how well they fit a solo first-time full-stack project.

---

## Option 1 — Node.js + Express + SQLite

A minimal backend-only API. Express is an unopinionated Node.js framework with
almost no built-in structure. SQLite is used directly via a library like `better-sqlite3`.

| | |
|---|---|
| Language | JavaScript |
| Frontend | Separate (not included) |
| Database access | Raw SQL or lightweight query builder |
| Type safety | None by default |
| Auto-generated API docs | No |

**Pros**
- Extremely simple to start — very few files needed
- Huge number of tutorials and Stack Overflow answers
- No compilation step, fast feedback loop
- Lightweight — nothing you didn't explicitly add

**Cons**
- No TypeScript by default — bugs show up at runtime, not during coding
- No frontend included — you'd need a separate React project
- No ORM — writing raw SQL means more boilerplate and more chances for mistakes
- No structure enforced — easy to write messy, hard-to-maintain code
- You manage two separate projects (API + frontend)

**Verdict for this project:** Too bare for a first full-stack project. Good for learning
HTTP basics in isolation but adds unnecessary friction when a UI is also required.

---

## Option 2 — Python + FastAPI + SQLite

A modern Python API framework. FastAPI automatically generates an OpenAPI (Swagger)
documentation page from your code. Uses Pydantic for data validation.

| | |
|---|---|
| Language | Python |
| Frontend | Separate (not included) |
| Database access | SQLAlchemy ORM or raw SQL |
| Type safety | Python type hints + Pydantic |
| Auto-generated API docs | Yes (built in) |

**Pros**
- Auto-generates OpenAPI spec — satisfies the assignment requirement for free
- Pydantic validation is excellent — catches bad input automatically
- Very readable, clean syntax
- Great if you already know Python

**Cons**
- Still no frontend — requires a separate React project
- Python environment setup can be frustrating (venv, pip, version conflicts)
- SQLAlchemy has a steep learning curve for beginners
- Two separate projects to manage and run simultaneously

**Verdict for this project:** Strong API framework, but splitting frontend and backend
into two projects adds cognitive overhead for a 2-week solo assignment.

---

## Option 3 — Next.js + TypeScript + Prisma + SQLite ✓ chosen

A full-stack framework where frontend (React) and backend (API routes) live in the
same project. Prisma handles the database with a clean schema file instead of raw SQL.

| | |
|---|---|
| Language | TypeScript |
| Frontend | Included (React, App Router) |
| Database access | Prisma ORM |
| Type safety | Full — frontend and backend share types |
| Auto-generated API docs | Via openapi-typescript tooling |

**Pros**
- One project, one repo, one `npm run dev` command — no juggling two servers
- TypeScript catches mistakes before you run the code
- Prisma schema is human-readable and generates the database automatically
- React frontend is built in — no separate setup
- App Router is the modern Next.js approach, worth learning
- Types can be shared between frontend and backend (no duplication)
- Large ecosystem, excellent documentation

**Cons**
- Steepest learning curve of the three — several new concepts at once
- App Router has some gotchas (server vs client components) for beginners
- Slightly more boilerplate to set up initially

**Verdict for this project:** Best overall fit. The higher upfront learning cost is
justified by having a single unified project, TypeScript safety, and a proper ORM.
The assignment itself is about learning AI-assisted development on a real stack —
this is the most realistic industry-like choice.

---

## Comparison summary

| Criteria | Node + Express | Python + FastAPI | Next.js + TS + Prisma |
|---|---|---|---|
| Frontend included | No | No | Yes |
| Type safety | No | Partial | Full |
| ORM quality | Low | Medium | High |
| Single project | No | No | Yes |
| Learning value | Low | Medium | High |
| Setup difficulty | Easy | Medium | Medium |
| Beginner friendly | Medium | Medium | Medium |

## Decision

**Chosen: Next.js + TypeScript + Prisma + SQLite**

The primary reasons:
1. Frontend and backend in one project reduces complexity for a solo 2-week assignment
2. TypeScript prevents an entire class of bugs before the code even runs
3. Prisma makes database work approachable without knowing SQL deeply
4. Next.js is widely used in industry — the learning investment has real value beyond this course

See `adr/0001-stack-decision.md` for the formal decision record.