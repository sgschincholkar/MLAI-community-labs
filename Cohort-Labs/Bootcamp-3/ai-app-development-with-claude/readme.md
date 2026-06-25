# AI App Development with Claude Code

A hands-on bootcamp that takes you from zero to a deployed, production-ready AI application — using Claude Code to plan, build, secure, and ship every step of the way.

You will build **ContractIQ**: a full-stack web app where users upload contract PDFs and receive an AI-powered breakdown of every clause that matters — what it says, where it appears, and how confident the model is in its reading.

No prior AI development experience required. Each lesson builds directly on the previous one.

---

## Lessons

| # | Lesson | What You Do |
|---|---|---|
| 1 | [Project Foundation](#lesson-1--project-foundation) | Understand the problem, fork the starter repo, and set up your local environment |
| 2 | [Skills and the Design System](#lesson-2--skills-and-the-design-system) | Learn how Claude Code skills work and explore the design system that governs the app's UI |
| 3 | [Engineering Planning](#lesson-3--engineering-planning) | Use Plan Mode to generate the engineering document and implementation specs |
| 4 | [Building the Application](#lesson-4--building-the-application) | Scaffold the Next.js project, implement the app, set up Supabase, and run it in the browser |
| 5 | [Memory Layer](#lesson-5--memory-layer) | Give the assistant persistent memory so it can answer follow-up questions across sessions |
| 6 | [Security Foundation](#lesson-6--security-foundation) | Scan the codebase for vulnerabilities and auto-fix every issue before shipping |
| 7 | [Deployment](#lesson-7--deployment) | Push to GitHub and deploy the live app to Netlify |

---

## Lesson 1 — Project Foundation

**Folder:** [`01-project-foundation`](./01-project-foundation/readme.md)

Introduces the problem ContractIQ solves and the application you will build throughout the bootcamp. You fork the `dev-os` starter repo, clone it to your machine, open it in VS Code, and read the Product Requirements Document to understand what you are building and why before writing any code.

**What you walk away with:** a local copy of the starter repo, a clear mental model of the product, and VS Code open and ready.

---

## Lesson 2 — Skills and the Design System

**Folder:** [`02-skills-and-design-system`](./02-skills-and-design-system/readme.md)

Explains what Claude Code skills are and why they matter: saved instruction sets that make Claude behave consistently across every session and every teammate. You explore the five skills in the project (`frontend-setup`, `engineering-planner`, `implementation-specs`, `security-fix`, and `design-system`) and review the design tokens, color palette, and typography rules in `docs/design.md` that will govern the UI.

**What you walk away with:** a clear understanding of how skills work and the design constraints the app must follow.

---

## Lesson 3 — Engineering Planning

**Folder:** [`03-engineering-planning`](./03-engineering-planning/readme.md)

Introduces Plan Mode — Claude Code's read-only planning mode that lets the AI think through architecture without touching any files. You run `/engineering-planner` to produce a high-level architecture document, then `/implementation-specs` to generate file-by-file implementation specs. These two documents become the blueprint every future lesson builds from.

**What you walk away with:** `docs/engineering/engineering-doc.md` and `docs/engineering/implementation-specs.md` — the authoritative plan for the entire application.

---

## Lesson 4 — Building the Application

**Folder:** [`04-building-the-application`](./04-building-the-application/readme.md)

The main build lesson. You run four prompts in sequence: scaffold the Next.js folder structure, implement the full application from the engineering documents, generate the database SQL schema, and load it into a live Supabase project. By the end you have a running app in the browser connected to a real database with authentication working end-to-end.

**What you walk away with:** a fully working ContractIQ app running at `http://localhost:3000`, backed by a live Supabase database.

---

## Lesson 5 — Memory Layer

**Folder:** [`05-memory-layer`](./05-memory-layer/readme.md)

Solves the stateless API problem: by default, each message to the AI is a fresh call with no knowledge of what came before. You implement a memory layer that loads conversation history from Supabase before every API call, classifies each question as `contract`, `history`, or `both`, builds the right context window, and saves every turn back to the database. Follow-up questions, page refreshes, and return visits all work correctly after this lesson.

**What you walk away with:** a chat interface that remembers conversation history within and across sessions, with source attribution on every response.

---

## Lesson 6 — Security Foundation

**Folder:** [`06-security-and-production`](./06-security-and-production/readme.md)

Runs the `security-fix` skill, which scans the entire codebase for the most common vulnerabilities and fixes each one automatically — hardcoded secrets, `NEXT_PUBLIC_` prefixes on secret keys, API routes missing auth checks, error responses that leak stack traces, missing security headers, unsafe `eval`/`innerHTML` patterns, and a missing `.gitignore` entry for `.env.local`. At the end the skill presents a summary table of every issue found and fixed.

**What you walk away with:** a codebase with no hardcoded secrets, protected API routes, safe error handling, and security headers in place — ready to deploy.

---

## Lesson 7 — Deployment

**Folder:** [`07-deployment`](./07-deployment/readme.md)

Takes the app from your local machine to the internet. You check `.gitignore`, stage and commit your changes, and push to GitHub. Then you connect the repo to Netlify, configure the build settings, import your environment variables, and deploy. The final step updates `NEXTAUTH_URL` to the production Netlify URL so authentication redirects work correctly on the live site.

**What you walk away with:** a live, publicly accessible app at `https://your-app-name.netlify.app` that automatically redeploys on every push to `main`.

---

## What You Will Build

**ContractIQ** — a full-stack AI application with:

- PDF upload and AI-powered contract analysis
- Structured clause breakdown with page citations
- Multi-turn chat with persistent conversation memory
- Supabase database with Row Level Security
- Authentication with protected routes
- Security-hardened codebase
- Automatic CI/CD deployment via Netlify

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Next.js 14, TypeScript, Tailwind CSS |
| Database & Auth | Supabase (PostgreSQL + Auth) |
| AI | Claude API (Anthropic) |
| Deployment | Netlify |
| Planning & Build | Claude Code |
