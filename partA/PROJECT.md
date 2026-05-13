# Personal Task Tracker

## Overview

A full-stack personal productivity application for managing daily tasks. Built with Next.js, TypeScript, Prisma, and SQLite. The app provides a clean UI for creating, organizing, and tracking tasks with priorities, due dates, and labels — all running locally with no authentication required.

## Goals

- Practice full-stack development with Next.js App Router
- Learn TypeScript in a real project context
- Use Prisma ORM to interact with a SQLite database
- Build a functional, usable UI with React components
- Apply AI-assisted development workflow (F.CSM311 Lecture 13)

## Scope

### In scope
- Task CRUD (create, read, update, delete)
- Priority levels: Low, Medium, High
- Due date assignment per task
- Labels/tags (e.g. "work", "personal", "urgent")
- Filter tasks by status (all / active / completed)
- Filter tasks by priority
- Mark tasks as complete / incomplete
- Basic responsive layout

### Out of scope
- User authentication / login
- Multiple users
- File attachments
- Notifications or reminders
- Mobile app (web only)

## Features

1. Task list view — displays all tasks with status, priority badge, due date, and labels
2. Create / edit task — form with title, description, due date, priority, and label fields
3. Complete toggle — mark any task done/undone with a single click
4. Filter bar — filter by status (active/completed) and priority (low/medium/high)
5. Delete task — remove tasks with a confirmation step

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Next.js 14 (App Router) |
| Language | TypeScript |
| Database | SQLite via Prisma ORM |
| Styling | Tailwind CSS |
| Testing | Vitest + React Testing Library |

## Team

Solo project — student developer + Claude (AI assistant)

## Timeline

2 weeks (F.CSM311 Бие даалт 13 deadline)