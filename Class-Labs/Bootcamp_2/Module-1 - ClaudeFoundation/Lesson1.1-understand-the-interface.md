# Lesson 1.1 — Download the Project Repository

---

## Where You Are

You've installed Claude Code in Lesson 1.0. Before you go any further, you need to download the project repository — the folder that contains all the company context files you'll use throughout this bootcamp.

This is a one-time setup. Once it's done, every lesson that asks you to `@` reference a context file will work out of the box.

---

## What You'll Learn

- How to download the bootcamp project repository from GitHub
- How to extract it and locate it on your machine
- How to add the folder to Claude Code so Claude can see your files

---

## What's Inside the Repository

The repository contains the sample company context files for LegalGraph — the fictional Series A legal tech company we use throughout the bootcamp:

| File | What it contains |
|------|-----------------|
| `company-overview.md` | Company stage, ARR, team size, funding |
| `product-description.md` | Product features, tech stack, key metrics |
| `user-personas.md` | Jennifer (GC), David (Senior Associate), Rachel (Compliance Lead) |
| `competitive-landscape.md` | Key competitors and LegalGraph's positioning |
| `company-context.md` | Combined context file used in Lessons 2.3–3.1 |

> If you're using your own company instead of LegalGraph, you'll create equivalent files for your product in Lesson 1.3.

---

## Step 1 — Open the Repository

Open your web browser and go to the bootcamp repository:

**[https://github.com/sachin0034-tech/aipminterview-bootcamp-project-repo](https://github.com/sachin0034-tech/aipminterview-bootcamp-project-repo)**

---

## Step 2 — Download the ZIP File

1. Click the green **Code** button near the top right of the repository page
2. Click **Download ZIP** from the dropdown
3. The file (`aipminterview-bootcamp-project-repo-main.zip`) downloads to your default Downloads folder

![images](./images/context.png)

---

## Step 3 — Extract the ZIP

**Mac:**
1. Go to your Downloads folder
2. Double-click the ZIP file — it extracts automatically
3. You'll see a folder named `aipminterview-bootcamp-project-repo-main`

![images](./images/zip.png)

**Windows:**
1. Go to your Downloads folder
2. Right-click the ZIP file → **Extract All**
3. Choose a destination folder and click **Extract**
4. You'll see a folder named `aipminterview-bootcamp-project-repo-main`

---

## Step 4 — Add the Folder to Claude Code

Claude Code can only `@` reference files it can see. You need to add your project folder to the chat once so Claude has access to everything inside it.

**In Claude Code Desktop:**
1. Click the **+** button or the folder icon in the chat sidebar
2. Select the extracted folder: `aipminterview-bootcamp-project-repo-main`
3. The folder is now active — Claude can read any file inside it

![images](./images/folder.png)

> **This folder is your workspace for the entire bootcamp.** Everything you produce from this point forward — market research, user research, PRDs, mocks — will be saved here. When Lesson 2.3 tells you to run `/market-research` and save to `outputs/`, that `outputs/` folder gets created inside this workspace. When Lesson 3.1 generates your prototype, it saves to `mocks/` inside this workspace. When you `@` reference a file in any lesson, you're referencing something inside this folder. Add it once here — and keep it added every session.

**Confirm it worked** — type this in Claude Code:

```
List the files in my project folder.
```

Claude should list your context files including `company-overview.md`, `product-description.md`, `user-personas.md`, and `competitive-landscape.md`.

---

## What Happens Behind the Scenes

When you add a folder to Claude Code, it becomes the working directory for the session. Any file inside can be referenced with `@filename` — Claude reads the full file contents before responding.

This is why the setup matters: every lesson from 2.3 onward uses `@company-context.md`, `@outputs/...`, and other file references. If the folder isn't added, those references fail silently and Claude generates generic output instead of grounded, specific output.

---

## Your Action Items

1. Download the ZIP from the repository link above
2. Extract it to a location you'll remember (Desktop or Documents works well)
3. Add the folder to Claude Code Desktop
4. Confirm Claude can see the files — ask it to list the project folder contents

---

*Next: [Lesson 1.2 — Understanding Context](./Lesson1.2-Understanding-Context.md)*
