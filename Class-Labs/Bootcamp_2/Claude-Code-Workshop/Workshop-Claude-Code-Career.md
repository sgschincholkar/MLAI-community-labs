# Claude Code Workshop — Build Your Personal AI Career Coach

![Claude download page](images/1.png)

---

## Index

- [Claude Code Workshop — Build Your Personal AI Career Coach](#claude-code-workshop--build-your-personal-ai-career-coach)
  - [Index](#index)
  - [The Workshop We're Doing Today](#the-workshop-were-doing-today)
  - [Prerequisites — Before You Start](#prerequisites--before-you-start)
    - [Step 1 — Create a project folder on your machine](#step-1--create-a-project-folder-on-your-machine)
    - [Step 2 — Download the template and add it to your folder](#step-2--download-the-template-and-add-it-to-your-folder)
    - [Step 3 — Add your resume to the folder](#step-3--add-your-resume-to-the-folder)
  - [Part 1 — Make Claude Remember You (CLAUDE.md)](#part-1--make-claude-remember-you-claudemd)
    - [The Problem](#the-problem)
    - [There Are Two CLAUDE.md Files. Both Matter.](#there-are-two-claudemd-files-both-matter)
    - [Step 1 — Build Your Global CLAUDE.md From Your Resume](#step-1--build-your-global-claudemd-from-your-resume)
    - [Concept: Passing Context With @](#concept-passing-context-with-)
    - [Step 2 — Build Your Local CLAUDE.md for This Job Search](#step-2--build-your-local-claudemd-for-this-job-search)
    - [The `askUserQuestion` Tool](#the-askuserquestion-tool)
    - [What Just Happened](#what-just-happened)
  - [Part 2 — Build Your Job Strategy Skill](#part-2--build-your-job-strategy-skill)
    - [The Problem This Solves](#the-problem-this-solves)
    - [Concept: What Is a Skill?](#concept-what-is-a-skill)
    - [Step 1 — Create the Job Strategy Skill](#step-1--create-the-job-strategy-skill)
    - [Step 2 — Run the Skill](#step-2--run-the-skill)
    - [What You Just Built](#what-you-just-built)
  - [Part 3 — Control Your Sessions Like a Pro (Slash Commands)](#part-3--control-your-sessions-like-a-pro-slash-commands)
    - [The Story So Far](#the-story-so-far)
    - [1. `/cost` — See Exactly What This Session Has Cost](#1-cost--see-exactly-what-this-session-has-cost)
    - [2. `/context` — See Exactly What Claude Can See Right Now](#2-context--see-exactly-what-claude-can-see-right-now)
    - [3. Planning Mode — Think Before Acting](#3-planning-mode--think-before-acting)
    - [4. Switch Models to Match the Task](#4-switch-models-to-match-the-task)
    - [The Full Slash Command Reference](#the-full-slash-command-reference)
  - [The Full Picture](#the-full-picture)
  - [What You've Learned](#what-youve-learned)
    - [Part 1 — CLAUDE.md](#part-1--claudemd)
    - [Part 2 — Skills](#part-2--skills)
    - [Part 3 — Session Control](#part-3--session-control)
  - [Your Next Actions](#your-next-actions)

---

## The Workshop We're Doing Today

You just installed Claude Code. You've poked around, maybe run a few prompts. And now you're wondering: *how do I actually make this useful for me — not just for code, not just for PMs, but for my career?*

That's what this workshop is about.

By the end, you'll have:
- A Claude that already knows who you are every time you open it
- A personal job strategy coach you can trigger with a single command
- Full control over cost, context, and complexity — so you're never flying blind

We're going to go step by step. Each section builds on the last. Don't skip ahead.

---

## Prerequisites — Before You Start

Before running any prompts, get your environment set up. This takes about 5 minutes.

---

### Step 1 — Create a project folder on your machine

Create a dedicated folder for this job search. This is where your `CLAUDE.md`, resume, and strategy files will live.

Or just right-click on your Desktop or Documents in Finder/Explorer → New Folder → name it `job-search-project`.

---

### Step 2 — Download the template and add it to your folder

We've provided a starter skill template to get you going.

**[Click here to download the template →](https://pragyaallc-my.sharepoint.com/:t:/g/personal/sachin_parmar_legalgraph_ai/IQCjBAO9MnkySpOfRsjl-PaBAdBhS3druHbIeNfX6WavXjI?e=jAU06C)**

Once downloaded, move the file into the folder you just created. Your folder should now look like this:

```
job-search-project/
└── job-strategy.md     ← the template you just downloaded
```

---

### Step 3 — Add your resume to the folder

Add your resume in the same folder.

```
job-search-project/
├── job-strategy.md     ← template
└── my-resume.md        ← your resume (add this now)
```

> **Why this matters:** When you type `@my-resume.md` in a Claude Code prompt, Claude reads the full contents of that file directly into context — no copy-pasting required. But the file must exist in the folder you're working in. Add it now before proceeding.

---

## Part 1 — Make Claude Remember You (CLAUDE.md)

### The Problem

Here's what happens without CLAUDE.md:

You open Claude Code. You paste your resume. You explain your situation. You ask for job strategy advice. Claude gives you something decent. You close the session.

Tomorrow you open Claude Code again. It knows nothing. You're back to square one.

This is the core frustration with AI tools: **they're stateless by default.** Every session is a blank slate.

CLAUDE.md fixes this. It's a file Claude reads automatically at the start of every session — so you never have to re-introduce yourself again.

---

### There Are Two CLAUDE.md Files. Both Matter.

| | Global CLAUDE.md | Local CLAUDE.md |
|---|---|---|
| **Location** | `~/.claude/CLAUDE.md` on your machine | `./CLAUDE.md` in your project folder |
| **What it holds** | Who you are, how you work, your preferences | Context specific to this project or goal |
| **When it loads** | Every session, everywhere | Only when you're in this folder |
| **Think of it as** | Your permanent identity layer | Your project briefing doc |

You build **global first**. Your identity doesn't change project to project. Then you layer the local file on top for whatever you're working on right now.

When Claude starts, it loads both. Global identity + local context. Together, automatically.

---

### Step 1 — Build Your Global CLAUDE.md From Your Resume

> **Before running this step — complete Prerequisites first:**
> 1. Create your project folder
> 2. Add your resume as `my-resume.md` inside that folder
> 3. Add the strategy template (`job-strategy.md`) to the same folder
> 
>
> Your folder should look like this before you continue:
> ```
> job-search-project/
> ├── my-resume.md        ← your resume
> └── job-strategy.md     ← downloaded template
> ```

Here's the concept: instead of writing your global CLAUDE.md by hand, you're going to give Claude your resume and let it figure out what to write. You supply the raw material, Claude structures it into a persistent identity layer.

Instead of pasting your resume as text, use `@my-resume.md` — Claude Code reads the file directly. Type this into Claude Code:

Open Claude Code and attach the folder that you have created 

![Claude download page](images/2.png)


**The meta prompt — paste this into Claude Code:**

```
@my-resume.md

Use my resume above to write my global CLAUDE.md — 
the file that tells Claude who I am, how I work, and what I'm trying to accomplish, 
so every future session starts with full context about me.

Include:
- My background and current role/stage
- My core skills and domain expertise
- My career goals and what I'm optimizing for
- How I like to work and communicate (concise, structured, no fluff)
- What kind of help I'll typically be asking for

Write this as a tight, scannable CLAUDE.md — bullet points, no filler. 
Claude should be able to read this and immediately know who I am 
and how to be most useful to me.

After writing it, save the result to ~/.claude/CLAUDE.md
```

> **What `@my-resume.md` does:** instead of `[PASTE YOUR RESUME HERE]`, typing `@my-resume.md` tells Claude Code to open and read that file automatically. Claude sees the full resume — you don't copy anything.

---

### Concept: Passing Context With @

`@` is one of the most powerful things in Claude Code. When you type `@filename`, you're passing the full file contents into Claude's context for that prompt. Claude doesn't just know the file exists — it reads it.


You're not copy-pasting anything. You're pointing Claude at two sources of truth and asking it to synthesize.

**Three ways to pass context in Claude Code:**
- For your identity → CLAUDE.md (loaded automatically every session)
- For specific files → `@filename` inline in any prompt
- For structured workflows → skills (embed `@` references inside the skill file so they load automatically)

You can even put `@` references inside skill files. If your `/job-strategy` skill should always load your resume, add `@my-resume.md` as the first line of the skill file — every run loads your resume without you typing anything.

---

**What Claude produces (example):**

```markdown
# About Me

- Software engineer, 4 years experience, currently IC2 at a Series B fintech
- Strong in Python, backend systems, some ML exposure
- Transitioning toward ML engineering / AI product roles
- Actively job searching — targeting senior IC or tech lead roles at AI-first companies

## What I'm Optimizing For
- Break into ML engineering without going back to school
- Land at a company where I can grow into AI product work
- Relocate from Austin to SF or remote

## How I Work
- Direct, structured communication — no filler
- I think in systems and trade-offs
- When uncertain about my situation, ask — don't guess

## What I'll Be Asking Claude For
- Job strategy and career planning
- Interview prep (behavioral + technical)
- Resume and LinkedIn feedback
- Understanding AI/ML roles and market landscape
```

Once Claude saves this file, it lives at `~/.claude/CLAUDE.md` permanently.

**Test it immediately.** Open a new Claude Code session and run:

```
What do you know about me? Summarize who I am and what I'm trying to accomplish.
```

If the global file loaded, Claude will describe you accurately — without you saying a word. That's the moment it clicks.

![alt text](./images/3.png)

---

> **Can't find the file?** Hidden directories don't show in Finder by default.
> - **Mac:** Press `Cmd + Shift + .` in Finder to show hidden files
> - **Terminal:** Run `cat ~/.claude/CLAUDE.md` to see the contents
> - **From Claude Code:** Just ask — *"Show me my global CLAUDE.md"* — Claude will read it for you

---

### Step 2 — Build Your Local CLAUDE.md for This Job Search

OK, so Claude now knows who you are globally. Good. But your current goal — this job search — has specific context that doesn't belong in a global file. The companies you're targeting. The roles you want. Your constraints. Your timeline.

That's what your local CLAUDE.md is for.

---

### The `askUserQuestion` Tool

Before running the prompt, understand what will happen when you do.

Your resume captures your past. But your local CLAUDE.md needs to capture your *current situation* — timeline, location constraints, comp floor, how far along you are in the search. That context isn't in a resume. Claude has to ask.

That's what `askUserQuestion` does. It's a built-in Claude Code tool that **pauses generation and asks you a direct question** before proceeding. Instead of guessing or making assumptions, Claude collects what it needs — one question at a time — then generates output grounded in your actual answers.

**Why this matters:**
- A CLAUDE.md written from assumptions is generic. One written from your answers is specific.
- `askUserQuestion` is what separates "Claude gave me a template" from "Claude wrote something that's actually about me."
- You'll see this same tool used in the `/job-strategy` skill in Part 2 — it's the pattern that makes skills feel like real conversations.

---

Now run this prompt. Notice the last instruction — it tells Claude to use `askUserQuestion` to collect missing context before writing anything:

```
@my-resume.md

Using my resume above, write the local CLAUDE.md for my current job search project.

Before writing anything, use the askUserQuestion tool to ask:
1. target timeline — when do I need an offer by?
2. location preference — remote, specific cities, or open to relocation?
3. compensation floor — minimum base salary I'll consider
4. current search stage — just starting, actively applying, or already interviewing?

Then write the CLAUDE.md using both my resume and my answers. Include:
- My target roles (be specific — titles I should be applying for given my background)
- Target companies (if I haven't specified, suggest 5-8 that match my profile)
- My constraints: timeline, location, compensation floor, search stage
- Working instructions for this project: when I ask for job strategy, always reference my actual experience. Don't give generic advice.

Save the result to ./CLAUDE.md in this folder.
```

![alt text](./images/4.png)

**Here's what that interaction looks like when you run it:**

> **Claude:** *Before I write your local CLAUDE.md, what's your target timeline — are you aiming to have an offer in hand within 30 days, 90 days, or by end of year?*

You answer. Claude follows up:

> **Claude:** *Got it. Location — are you remote-only, targeting specific cities, or open to relocation?*

You answer. Claude continues:

> **Claude:** *And your compensation floor — what's the minimum base salary you'd accept?*

You answer. One more:

> **Claude:** *Last one — where are you in the search right now? Just starting, actively applying, or already in interviews somewhere?*

Once you've answered, Claude writes and saves `./CLAUDE.md` — using your resume *and* your answers together. Nothing assumed. Nothing generic.

**What this produces:**

```markdown
## Job Search Context

**Candidate:** [Your Name] — Backend Engineer → ML Engineering

### Target Roles
- Machine Learning Engineer (IC3/Senior)
- AI/ML Platform Engineer
- ML Infrastructure Engineer
- (Stretch) Staff Engineer at AI-first company

### Target Companies
- Anthropic, OpenAI, Cohere (AI-first)
- Stripe, Databricks, Scale AI (ML-heavy engineering culture)
- Series B-D AI startups with ML infra needs

### Search Status
- Resume: ready
- Applying: active
- Timeline: offer in hand by Q3

### Constraints
- Remote-first or SF Bay Area
- Comp floor: $X base
- Not open to pure research roles — want applied ML / product-adjacent

## Working Instructions
- When giving job strategy advice, ground it in my actual resume — not generic advice
- Call out gaps between my background and target roles explicitly
- Prioritize actionable next steps over theory
```

Now when you open Claude Code in this folder, it loads both files:
1. Your global identity (`~/.claude/CLAUDE.md`)
2. Your job search context (`./CLAUDE.md`)

Every prompt you run — automatically briefed.

---

### What Just Happened

You used Claude to generate the files that will brief Claude forever. That's the leverage. You did this once, and now every future session starts with full context. No re-explaining, no copy-pasting your resume, no generic responses that ignore who you actually are.

Global CLAUDE.md = you.
Local CLAUDE.md = your current mission.

Both load silently. You never have to think about them again — unless you want to update them.

---

## Part 2 — Build Your Job Strategy Skill

### The Problem This Solves

You've built the context layer. Now let's build the action layer.

Here's what happens without a skill: every time you want job strategy help, you write a prompt that includes your ask, explains your situation (again), specifies the format you want, and describes how thorough to be. 60 words of setup before you even get to your actual question.

With a skill, you type `/job-strategy` and Claude does the whole thing — asks you the right questions, uses your resume as context, produces a structured plan.

You define the workflow once. You run it forever.

---

### Concept: What Is a Skill?

A skill is a `.md` file stored in a specific folder. The filename becomes the command. The file contents become the prompt Claude receives — automatically, every time you run it.

| File | Command | What it does |
|------|---------|--------------|
| `~/.claude/commands/job-strategy.md` | `/job-strategy` | Runs your full job strategy workflow |
| `~/.claude/commands/interview-prep.md` | `/interview-prep` | Preps you for a specific role |

Two storage locations:

| Location | Scope | Use for |
|----------|-------|---------|
| `~/.claude/commands/` | Every session, everywhere | Your personal career toolkit |
| `./.claude/commands/` | This project only | Context-specific workflows |

---

### Step 1 — Create the Job Strategy Skill

Paste this into Claude Code. It will create the skill file for you:

> **Note:** Replace `@creatingAIJobstartegt.pdf` with the template you downloaded in the prerequisites step. Reference it using `@your-filename` (e.g., `@job-strategy.md`).

![alt text](./images/6.png)

```
Strategy Template: @job-strategy.md

Create a skill in file ~/.claude/commands/job-strategy.md with exactly the following content:

## Goal
This skill helps users generate **personalized job search strategies using the template attached to you**.

## Behavior
Trigger this skill whenever a user asks about:
- Job strategy
- Career planning
- Job switch
- Job preparation
- Breaking into a role/company

## Instructions
- Use the `askUserQuestion` tool to gather required information from the user.
- You MUST collect the following before generating any strategy:
  - Resume (text or file)
  - LinkedIn profile
- Do NOT generate any strategy until both Resume and LinkedIn profile are provided.
- After collecting the required inputs, continue asking follow-up questions using the `askUserQuestion` tool to improve context, such as:
  - Target role(s)
  - Target company (if any)
  - Experience level
  - Constraints (time, location, timeline, etc.)
- Keep asking questions until you have sufficient context.

## Rules
- Do NOT perform any evaluation or scoring
- Do NOT generate generic responses
- Always prioritize better context before answering
- Think like a career coach + recruiter
```

---

### Step 2 — Run the Skill

Now trigger it:

```
I will transition into an ______ role at ____ level by building real AI products in [domain], creating strong public proof of work, and consistently applying with targeted signals, aiming to secure the role in [X months] and reach [$X compensation] within____ time.”

```

![alt text](./images/7.png)


Watch what happens. Claude doesn't immediately generate a strategy. Instead, it asks you questions — one at a time, using the `askUserQuestion` tool. This is deliberate: the skill is designed to collect before it produces.

**Here's what `askUserQuestion` looks like in action:**

Claude will pause the response and ask you something like:
> *"Before I build your strategy, I need a few things. Can you paste your resume here, or reference it with @my-resume.md if you've already saved it?"*

You answer. Claude follows up:
> *"Got it. And your LinkedIn — can you share the URL or a summary of your profile?"*

You answer. Claude continues:
> *"What specific roles are you targeting? Give me the exact job titles you're applying for."*

This continues until Claude has everything it needs. Only then does it generate the strategy — grounded in your actual background, not a generic template.

---

### What You Just Built

Let's recap. You now have:
1. A global CLAUDE.md that tells Claude who you are in every session
2. A local CLAUDE.md that tells Claude your current job search context
3. A `/job-strategy` skill that asks the right questions and produces a structured, personalized plan

Run `/job-strategy` any time you need a fresh strategy, want to pressure-test a new direction, or are prepping for a specific company. Every run uses your actual background. Every run asks before it generates.

---

## Part 3 — Control Your Sessions Like a Pro (Slash Commands)

### The Story So Far

You've got context (CLAUDE.md). You've got skills (`/job-strategy`). Now let's talk about the third layer: **session control**.

Here's what happens without it: you're 45 minutes into a session, you've loaded your resume, run three skills, had a long conversation — and suddenly Claude's responses get shorter, less specific, a little off. Or you get an "out of context" error. Or your bill at the end of the month surprises you.

These four slash commands prevent all of that.

---

### 1. `/cost` — See Exactly What This Session Has Cost

**What it does:** Shows you token usage and estimated dollar cost for your current session.

**Why it matters:** Every prompt costs tokens. Every `@` file you load costs tokens. Long conversations cost tokens. Without `/cost`, you're spending blind.

**Run it:**
```
/cost
```

**What you see:**

| Metric | What it means |
|--------|--------------|
| Input tokens | Your prompts + all `@` files loaded + CLAUDE.md |
| Output tokens | Everything Claude generated |
| Cache read tokens | Tokens served from cache (cheaper) |
| Estimated cost | Total $ for this session |

**Good habit:** Run `/cost` after loading several files or after a long skill run. If input tokens are high, it's because you've loaded large files. That's useful to know before you chain five more prompts.

```
/cost
```

Note the number. Then load a large file:

```
@my-resume.md
What are my top skills?
```

Run `/cost` again. Watch the input token count jump. That's the cost of loading context. Now you know.

---

### 2. `/context` — See Exactly What Claude Can See Right Now

**What it does:** Shows you what's currently loaded in Claude's active context window — which files are in scope, how full the window is, and what Claude can actually "see."

**Why it matters:** Context windows are finite. After a long session, the window fills up. When it does, older parts of your conversation start dropping out. Claude might "forget" something you told it an hour ago. `/context` shows you where you stand before that happens.

**Run it:**
```
/context
```

![alt text](./images/8.png)


**What to check:**
- Is your CLAUDE.md loaded? (It should be — it loads automatically)
- Are the `@` files you referenced still in context?
- How full is the window? (If it's over 70%, think about compressing)

**What to do when context is full:**

```
/compact
```

`/compact` compresses your conversation history — it summarizes what happened so far and clears space for what's next. You keep the thread of the conversation, but Claude has room to work again.

> **Important distinction:**
> - `/compact` — compress and continue. History is summarized, not lost.
> - `/clear` — wipe everything and start fresh. Use this only when you actually want to start over.

Don't confuse them. `/clear` is irreversible.

---

### 3. Planning Mode — Think Before Acting

**What it does:** Before Claude takes any action, it shows you a plan and waits for your approval. Nothing happens until you say go.

**Why it matters:** When you're running complex workflows — generating strategy documents, saving files, chaining multiple prompts — it's easy to end up with outputs you didn't intend. Planning mode forces a pause between "here's what I'll do" and "doing it."

![alt text](./images/9.png)



```
@my-resume.md

Plan mode: I want you to build me a complete job search package for a Senior ML Engineer role at Anthropic.

Before doing anything, lay out your plan — what you'll create, in what order, and what files you'll save. Wait for my approval before starting.
```

**What Claude returns (before touching anything):**

```
Here's my plan. I'll wait for your go-ahead before executing any of it.

Step 1 — Gap analysis
  Read @my-resume.md and your CLAUDE.md
  Identify where your background matches Anthropic's Senior ML Engineer bar
  Flag the gaps that will come up in screening

Step 2 — Positioning statement
  Write a 2-sentence positioning statement tailored to Anthropic's research culture
  Save to ./anthropic-positioning.md

Step 3 — Job strategy document
  Run the full strategy template from your /job-strategy skill
  Ground every section in your actual experience — no generic advice
  Save to ./anthropic-strategy.md

Step 4 — 30-day action plan
  Map the specific steps to get from "applied" to "offer"
  Prioritize by impact, not effort
  Save to ./anthropic-30-day-plan.md

Shall I proceed?
```

You review it. You say *"skip step 2, start from step 3"* or *"looks good, go"* — and only then does Claude start working.

**Why this matters for your career workflow specifically:** skills save files. You don't always know exactly what a skill will generate until it runs. Planning mode lets you see the output structure and file names before anything lands on disk. No surprises.

**When to use planning mode:**
- Before running `/job-strategy` for the first time (see the full flow before it saves anything)
- When you're asking Claude to generate multiple files in one go
- When you're not sure if Claude understood your ask — see the plan, course-correct before it executes

---

### 4. Switch Models to Match the Task

**What it does:** Lets you switch between Claude models mid-session using the model selector in the Claude Code desktop app.

**Why it matters:** Different tasks warrant different models. Using Opus for everything is like driving a semi-truck to pick up groceries. Matching the model to the task saves money without sacrificing quality.

![alt text](./images/10.png)

**Model guide for career work:**

| Model | When to use it | Relative cost |
|-------|---------------|---------------|
| `claude-haiku-4-5` | Quick questions, short lookups, iteration | Cheapest |
| `claude-sonnet-4-6` | Most job strategy work, writing, analysis | Mid |
| `claude-opus-4-6` | Deep strategy, complex reasoning, high-stakes output | Most expensive |

**How to switch:** Click the model selector at the top of the Claude Code desktop app and choose the model that matches your task.

**The practical workflow:**
1. Start a session with Sonnet (default, solid for most things)
2. If you're doing quick iteration — "give me 5 company names to target" — switch to Haiku
3. If you're doing something high-stakes — "review my full strategy and tell me what I'm missing" — switch to Opus
4. Switch back to Sonnet for the rest of the session

One session, multiple models. You're in control.

---

### The Full Slash Command Reference

| Command | What it does | When to use it |
|---------|-------------|---------------|
| `/cost` | Token usage and cost breakdown | After heavy context loading; before long sessions |
| `/context` | What's in Claude's active window | When responses feel off; before complex generations |
| `/compact` | Compress history, keep the thread | When context window is over 70% full |
| `/clear` | Wipe everything, start fresh | When you genuinely want a new session |
| `/plan` | Show the plan, wait for approval | Before multi-step or file-writing tasks |
| `/model` | View or switch active model | Matching model to task complexity |
| `/help` | Full list of commands | When you can't remember a command |
| `/init` | Auto-generate CLAUDE.md for a folder | When joining a new project |

---

## The Full Picture

Let's zoom out. Here's what you've built across all three parts:

```
You open Claude Code
        ↓
Claude loads ~/.claude/CLAUDE.md        ← your identity, always
        ↓
Claude loads ./CLAUDE.md                ← your job search context, this folder
        ↓
Both in context — session starts fully briefed
        ↓
You run /job-strategy
        ↓
Claude uses askUserQuestion to collect your resume + LinkedIn
        ↓
Claude asks follow-up questions until it has enough context
        ↓
Claude generates a personalized strategy using the template
        ↓
You check /context if something feels off
        ↓
You switch models via the desktop app selector for quick follow-up questions
        ↓
Session done — next session starts exactly where your context is, automatically
```

This is the system. Identity layer + skills layer + control layer. Each one reinforces the others.

---

## What You've Learned

### Part 1 — CLAUDE.md
- **Why there are two files:** global (`~/.claude/CLAUDE.md`) holds your permanent identity; local (`./CLAUDE.md`) holds your current project context. Both load automatically.
- **How to generate them from your resume:** you gave Claude raw material, it structured your identity. You didn't write the file — you briefed the system.
- **How `@` works:** `@filename` passes full file contents into context for that prompt. The local CLAUDE.md prompt uses `@my-resume.md` to generate grounded output, not guesses.

### Part 2 — Skills
- **Skills are `.md` files in `commands/`:** the filename becomes the command, the file contents become the prompt.
- **`askUserQuestion` is how skills collect before generating:** no strategy until you have the resume and LinkedIn. Claude asks, you answer.
- **`@` is how you pass context:** point Claude at files instead of copy-pasting. Use it inline, or embed it inside skill files so it loads automatically.
- **Two storage locations:** `~/.claude/commands/` for global personal skills; `./.claude/commands/` for project-scoped skills you can share.

### Part 3 — Session Control
- **`/cost`:** see exactly what you've spent — tokens and dollars — at any point in the session.
- **`/context`:** see what Claude can currently see and how full the window is. Use before complex generation tasks.
- **`/compact` vs `/clear`:** compress and continue vs. wipe and start over. Don't confuse them.
- **Planning mode:** Claude shows its plan and waits for approval before acting. Use for multi-step tasks.
- **Model switching:** match the model to the task via the desktop app selector. Haiku for quick iteration, Sonnet for most work, Opus for high-stakes strategy.

---

## Your Next Actions

Now that you have the system set up:

1. **Test your CLAUDE.md** — open a new session, ask "what do you know about me?" If it works, you're set.
2. **Run `/job-strategy`** — go through the full flow. See how the questions land. Edit the skill if the output isn't what you need.
3. **Switch your model and enable plan mode from the desktop app** — use the model selector in the Claude Code desktop app to switch between Haiku, Sonnet, and Opus. Toggle plan mode on when running multi-step tasks so you can review Claude's plan before it executes.

The system is built. Now you use it.

---
