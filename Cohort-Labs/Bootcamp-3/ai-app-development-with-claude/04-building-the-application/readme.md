[← Lesson 3](../03-engineering-planning/readme.md) | **Lesson 4** | [Lesson 5 →](../05-memory-layer/readme.md)

---

# Lesson 4 — Building the Application

## Where We Are

By this point you have:

- **Lesson 1** — Forked the `dev-os` starter repo, cloned it to your machine, and opened it in VS Code.
- **Lesson 2** — Explored the five skills and reviewed the design system in `docs/design.md`.
- **Lesson 3** — Used Plan Mode to run `/engineering-planner` and `/implementation-specs`, producing the engineering documents in `docs/engineering/`.

Now it is time to build. This lesson walks through four prompts that take you from an empty folder to a running application connected to a live database.

---

## What You Will Do in This Lesson

| Step | What Happens |
|---|---|
| Prompt 1 | Scaffold the Next.js folder structure |
| Prompt 2 | Implement the application based on the engineering documents |
| Prompt 3 | Generate the database SQL schema |
| Prompt 4 | Load the schema into Supabase and connect the app |

By the end, you will have a working app you can open in a browser.

---

## Before You Start — Set Up Supabase

The application uses **Supabase** as its database and authentication layer. You need to create a project there before running the prompts, because the prompts will ask for your credentials.

### Create a Supabase Account

1. Go to [supabase.com](https://supabase.com) and click **Start your project**.
2. Sign in with GitHub (recommended) or create an account with your email.
3. Once logged in, click **New project**.
4. Give the project a name (e.g. `contractiq`), choose a region close to you, and set a strong database password. Save the password somewhere — you will need it later.
5. Click **Create new project**. Supabase will take about 60 seconds to spin up.

### Copy Your Credentials

You need three values from Supabase. Here is where to find them:

**Project URL**
1. Go to your project dashboard.
2. Click **Project Settings** in the left sidebar.
3. Click **API**.
4. Copy the value under **Project URL**. It looks like `https://xyzxyzxyz.supabase.co`.

**Anon Key (public)**
On the same **API** settings page, scroll down to **Project API keys**.
Copy the value next to **`anon` `public`** — also listed as the **legacy anon key**. This is safe to use in browser code.

**Service Role Key (secret)**
On the same page, copy the value next to **`service_role`**. This key bypasses Row Level Security — keep it out of your frontend code and never commit it to GitHub.

Set these aside. You will add them to your `.env` file at the end of this lesson.

---

## Prompt 1 — Scaffold the Folder Structure

Open a Claude Code session in your project folder and run:

```
Use @skills/frontend-setup/SKILL.md to set up the frontend foundation for this project.
```

> **Note:** Claude may ask whether to create a new subfolder or work inside the current directory. Choose **current directory** and continue.

### What This Does

The `frontend-setup` skill creates the complete Next.js 14 folder structure — pages, components, API routes, and configuration files — with the design system already baked in. Think of it as building the empty shell of the house before any furniture goes in: every room exists, every door is in the right place, and the wiring is ready.

**What you get after this prompt:**

```
apps/web/
├── app/
│   ├── (auth)/
│   │   ├── login/
│   │   └── signup/
│   ├── (dashboard)/
│   │   └── dashboard/
│   └── layout.tsx
├── components/
│   ├── ui/
│   └── shared/
├── lib/
│   ├── supabase/
│   └── utils/
├── types/
├── styles/
├── public/
├── .env.local.example
├── next.config.ts
├── tailwind.config.ts
└── package.json
```

The design tokens from `docs/design.md` are loaded into Tailwind so your brand colors and fonts are available from the first component you write. The Supabase client is configured and waiting for your credentials.

Review the file tree once the skill finishes. If anything looks off, describe the issue and Claude will correct it before you move on.

---

## Prompt 2 — Implement the Application

Once the folder structure looks right, paste this prompt into Claude Code:

```
Based on docs/engineering/engineering-doc.md and docs/engineering/implementation-specs.md, start implementing the application.

Before writing any code:
- Read and understand the Engineering Document.
- Read and understand all feature specifications.
- Identify dependencies between features.
- Create an implementation plan and execution order.

Implementation Rules:
- Follow the architecture defined in the Engineering Document.
- Follow the design system defined in docs/design-system.md.
- Follow all folder structure and naming conventions.
- Use TypeScript throughout the application.
- Create reusable and maintainable components.
- Write production-ready code only.
- Do not leave TODO comments or placeholder implementations.
- Implement proper loading, error, and empty states.
- Implement validation and security requirements defined in the specs.
- Keep code modular and scalable.
- Use the claude-haiku-4-5-20251001 model.
```

### What This Does

Claude reads both engineering documents — the high-level architecture and the file-by-file implementation specs — before writing a single line of code. It maps dependencies between features, then builds them in the correct order so nothing references something that does not exist yet.

The result is production-quality code: typed, styled to the design system, with loading states, error boundaries, and validated inputs throughout.

This prompt takes the most time. Claude may ask clarifying questions before it begins — answer them so it has full context. Do not interrupt mid-implementation unless something is clearly wrong.

---

## Prompt 3 — Generate the Database Schema

Once the application code is in place, run:

```
Create a database.sql file that contains all SQL statements required to set up the database for the application. Based on the Engineering Document and Implementation Specifications, generate a complete production-ready database schema.
```

### What This Does

Claude reads the data models in your engineering documents and writes a single `database.sql` file that creates every table, relationship, index, and Row Level Security policy the app needs. This file is ready to paste directly into Supabase.

---

## Prompt 4 — Load the Schema and Connect the App

### Run the SQL in Supabase

1. Open your Supabase project dashboard.
2. Click **SQL Editor** in the left sidebar.
3. Click **New query**.
4. Open `database.sql` in VS Code. Select all (`Cmd+A` on Mac, `Ctrl+A` on Windows). Copy.
5. Paste the SQL into the Supabase SQL Editor.
6. Click **Run** (or press `Cmd+Enter`).

Supabase will execute all the statements. When it finishes without errors, your database tables are live.

If you see an error, read the message — it usually names the exact line that failed. Common causes are a table being referenced before it is created (a foreign key ordering issue) or a typo in a policy name. Paste the error back into Claude Code and it will fix the specific line.

### Add Your Credentials to `.env`

Open `.env.local` in the root of your project (if it does not exist, rename `.env.local.example`). Add your three Supabase values:

```
NEXT_PUBLIC_SUPABASE_URL=https://xyzxyzxyz.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key-here
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key-here
```

Replace the placeholder values with the credentials you copied earlier.

> **Important:** `SUPABASE_SERVICE_ROLE_KEY` must never appear in browser-side code and must never be committed to GitHub. The `.env.local` file should already be listed in `.gitignore` — verify this before your first push.

---

## Test Your Application

Open a new terminal in VS Code (**Terminal > New Terminal**), then start the development server:


/note make sure you are in the woring frongedn dolrr 

```bash
npm run dev
```

Open `http://localhost:3000` in your browser and walk through these checks:

| Check | What to Look For |
|---|---|
| Home page loads | No blank screen, no console errors |
| Sign up works | Create a test account; confirm the user appears in Supabase **Authentication > Users** |
| Log in works | Sign in with the test account |
| Dashboard loads | Authenticated route renders correctly |
| Core feature works | Upload a file or trigger the main feature of the app |
| Database writes | Check the relevant table in Supabase **Table Editor** to confirm data was saved |

If anything fails, open the browser dev console (`F12`) and read the error. Most issues at this stage come from a missing environment variable or a table name mismatch between the SQL schema and the application code. Paste the error into Claude Code with the relevant file path and it will fix it.

---

## What You Have Built

At the end of this lesson you have:

- A Next.js 14 application with a complete production folder structure
- A live Supabase database with the full schema loaded and Row Level Security enabled
- Authentication wired end-to-end
- The core features of ContractIQ implemented and running in a browser

The next lesson adds the memory layer — giving the application the ability to remember user context across sessions.

---

## What You Learned

- **Supabase setup and credentials** — how to create a project, locate the three keys you need (URL, anon key, service role key), and why the service role key must stay server-side and out of version control.
- **The four-step build sequence** — scaffold folder structure → implement from engineering documents → generate SQL schema → load schema and connect credentials; each step depends on the previous one being complete.
- **Reading engineering documents before writing code** — Claude uses the architecture and implementation specs as a map so every file is placed correctly, every dependency is resolved in the right order, and nothing is left as a placeholder.
- **Loading a database schema into Supabase** — how to paste and run `database.sql` in the SQL Editor, and how to diagnose the two most common errors (foreign key ordering, table name mismatches).
- **End-to-end verification checklist** — testing home page load, sign-up, login, dashboard render, core feature, and database writes as a structured sequence rather than clicking around and hoping for the best.
- **Environment variable safety** — the difference between `NEXT_PUBLIC_` variables (safe in browser code) and secret keys that must only appear in server-side routes, and how `.gitignore` protects `.env.local` from accidental commits.

---

[← Lesson 3](../03-engineering-planning/readme.md) | **Lesson 4** | [Lesson 5 →](../05-memory-layer/readme.md)