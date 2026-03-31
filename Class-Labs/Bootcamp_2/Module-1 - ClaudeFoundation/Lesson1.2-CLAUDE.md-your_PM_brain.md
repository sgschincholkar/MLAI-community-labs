# Lesson 1.3 — Persistent Context in Claude Code: Building CLAUDE.md as a PM

![images](./images/claudecontext.png)

---

## Prerequisites

- Complete Module 0 and Lessons 1.1 and 1.2 before starting this lesson
- You'll need your company's context files for this lesson (`company-overview.md`, `product-description.md`, `user-personas.md`, `competitive-landscape.md`). If you don't have your own company, download the sample company files we're using in this lab and use those instead: **[Download Sample Company Files](./sample-company/)**

---

## What You'll Learn

- What CLAUDE.md is and why it exists
- The difference between global and project CLAUDE.md — and why you build global first
- How to build your personal working style that travels with you everywhere
- How to build your company context that loads for this project
- How Claude loads both together at the start of every session

---

## The Problem

Every time you start a new conversation with Claude, it knows nothing about you.

It doesn't know your company, your product, your users, your metrics, your templates, or your preferences. So you end up doing one of two things — both painful:

1. **You re-explain everything at the start of every conversation.** "So we're a B2B SaaS for legal teams, we have three personas — Jennifer, David, and Rachel — and our north star metric is..."
2. **You skip the context and Claude guesses.** It makes up features, invents competitors, uses the wrong tone, formats things you can't use.

CLAUDE.md is how you fix this. It's a persistent instruction file Claude reads at the start of every session — think of it as the onboarding doc you'd give a new hire on day one, except this one gets read every time, without complaint.

---

## There Are Two CLAUDE.md Files — And Order Matters


![images](./images/claudecontext.png)

Before you build anything, you need to understand that there isn't one CLAUDE.md. There are two, and they serve completely different purposes.

| | Global CLAUDE.md | Project CLAUDE.md |
|---|---|---|
| **Location** | `~/.claude/CLAUDE.md` on your machine | `./CLAUDE.md` in your project folder |
| **What it contains** | Your personal PM working style | Company context for this specific project |
| **Who sees it** | Just you | Anyone on the team via source control |
| **Loaded when** | Every Claude session, everywhere | Only when you're in this project folder |

**You build global first.** Your working style doesn't change project to project — how you want PRDs structured, how direct you want Claude to be, what frameworks you default to. Set it once, and it follows you everywhere.

Then you build the project file. That's where the company-specific context lives — LegalGraph's personas, metrics, competitive landscape, product details. It loads on top of your global file whenever you're working in this project.

When a session starts, Claude loads both. Your personal style plus the company context — together, every time.

---

## Step 1 — Build Your Global CLAUDE.md

Your global file lives at `~/.claude/CLAUDE.md`. It describes how you work, not what company you're at.

As a PM, this is where you put the things that are true regardless of which product you're building:
- How you like PRDs structured
- What prioritization framework you default to
- How direct you want Claude to be
- How you want research outputs formatted

Run this prompt to build it:

![images](./images/1.1.png)

```
Write my global CLAUDE.md — the file that tells Claude how I work as a PM, regardless of which company or project I'm in.

My working style:
- I'm a senior PM — skip the basics, get to the point
- When uncertain about product details, ask me — don't guess
- Default PRD template: Problem Statement → User Persona → Jobs to be Done → Success Metrics → Requirements → Open Questions
- Default prioritization framework: RICE scoring unless I say otherwise
- Always surface trade-offs explicitly — don't just recommend one path
- When I ask for research, structure it as: Market Size → Key Trends → Competitive Dynamics → Implications for Us, and end with "What We Still Don't Know"
- Output format: ## headers, bullet points, tables when comparing options
- Always end research outputs with an "Open Questions" section

Write this as a tight, scannable CLAUDE.md — this is my personal working style and should apply everywhere.

save the result to ~/.claude/CLAUDE.md
```

**What this produces:**

```markdown
# My PM Working Style

- Senior PM — skip the basics, get to the point
- When uncertain about product details, ask — don't guess

## PRDs
- Template: Problem Statement → User Persona → Jobs to be Done → Success Metrics → Requirements → Open Questions
- Always tie to a persona

## Prioritization
- Default: RICE scoring unless specified otherwise
- Always surface trade-offs explicitly — don't just recommend one path

## Research
- Structure: Market Size → Key Trends → Competitive Dynamics → Implications for Us
- End with: What We Still Don't Know

## Format Defaults
- ## for headers
- Bullets for lists
- Tables for comparisons
- "Open Questions" at the end of all research outputs
```

Once Claude runs the prompt, you'll see a confirmation like this:

> *Written to ~/.claude/CLAUDE.md. It covers: Identity — senior PM, skip the basics. Core behaviors — ask when uncertain, surface trade-offs, formatting defaults. Three templates — PRD, Research (with "What We Still Don't Know"), and RICE scoring table. This will apply globally across all projects and sessions.*

The file is now saved at `~/.claude/CLAUDE.md` and loads at the start of every Claude session you ever open — on any project, in any folder.

**Test it:** Open a new Claude Code session and run this:

```
What do you know about how I like to work as a PM? Summarise my working style.
```


![images](./images/1.2.png)

If the global file loaded correctly, Claude should describe your PRD template, RICE scoring preference, research structure, and tone — without you having to say anything.

---

**Can't find the file?** That's normal. `~/.claude/` is a hidden directory — your file explorer won't show it by default.

- **Mac Finder** — press `Cmd + Shift + .` to toggle hidden files
- **Mac Terminal** — run `ls ~/.claude/CLAUDE.md` to confirm it's there
- **Windows File Explorer** — go to View → Show → Hidden items to toggle hidden files
- **Windows Command Prompt** — run `dir %USERPROFILE%\.claude\CLAUDE.md` to confirm it's there
- **From Claude Code (any OS)** — just ask: *"Show me the contents of my global CLAUDE.md"* and Claude will read it for you

---

## Step 2 — Build Your Project CLAUDE.md

Now you build the company-specific layer. This is what makes Claude understand LegalGraph — the product, the users, the metrics, the competitive landscape.

This file lives inside your project folder as `./CLAUDE.md`. It loads on top of your global file whenever you're working in this project.

### How @ works in Claude Code

Before running the prompt, you need to understand the `@` symbol — one of the most important mechanics in Claude Code.

When you type `@filename` in the chat, you're passing that file's contents directly into Claude's context. Claude doesn't just know the file exists — it reads it. You're not copy-pasting. You're pointing Claude at a source of truth.

This is why adding your folder to the chat first matters. Claude can only `@` files it can see.

> **Note:** Add your project folder to the chat before running the prompt below. Make sure your four context files are saved there — `company-overview.md`, `product-description.md`, `user-personas.md`, and `competitive-landscape.md`.

### The prompt

```
@company-overview.md
@product-description.md
@user-personas.md
@competitive-landscape.md

Write the Company & Product section of my project CLAUDE.md using the context in the files above. Write this as a tight, scannable CLAUDE.md section — bullet points, no fluff. Claude should be able to read this and immediately understand what we do, who our users are, and where we are as a company.

Save the output to ./CLAUDE.md in this project folder.
```

> **What happens:** Claude reads all four files, generates the section, and saves it as `./CLAUDE.md` in your project folder. You'll see the file appear there once the prompt runs.

![images](./images/1.4.png)

**Example — filled in for LegalGraph:**

```
@company-overview.md
@product-description.md
@user-personas.md
@competitive-landscape.md

Write the Company & Product section of my project CLAUDE.md using the context in the files above. Write this as a tight, scannable CLAUDE.md section — bullet points, no fluff. Claude should be able to read this and immediately understand what LegalGraph does, who our users are, and where we are as a company.

Save the output to ./CLAUDE.md in this project folder.
```

**What Claude produces:**

```markdown
## Company & Product

**LegalGraph** — AI-powered contract review for in-house legal teams

### Company
- Stage: Series A — $12M raised
- Team: 35 people, Austin TX
- ARR: $3.8M | 85 paying customers | 45 enterprise accounts

### Product
- Core: AI clause extraction (200+ clause types), risk scoring (15 dimensions), playbook management
- Built on GPT-4 + Claude 3, fine-tuned on 500k+ legal contracts

### Key Metrics
- 94% AI extraction accuracy
- 3.5 hours saved per contract reviewed
- 55% activation rate (free → paid)

### User Personas
- Jennifer (General Counsel) — owns vendor risk, signs off on all contracts above $50k
- David (Senior Associate) — does day-to-day review, needs speed
- Rachel (Compliance Lead) — focused on regulatory clauses, GDPR, SOC 2
```

![images](./images/1.2.png)

---

## Step 3 — Add Working Instructions to Your Project CLAUDE.md

Company context tells Claude what you're building. Working Instructions tell Claude how to help you build it.

This is where you define the PM-specific rules that are unique to this product — which competitors exist, which personas to reference, how to frame prioritization decisions for LegalGraph specifically.

At this point `./CLAUDE.md` already exists from Step 2. This prompt adds the Working Instructions section to it — it doesn't create a new file, it appends to the one that's already there.

```

Write the "Working Instructions" section and append it to ./CLAUDE.md. This section tells Claude how to behave when helping me with PM work on this product.

My defaults:
- When writing PRDs, use our template: Problem Statement → User Persona → Jobs to be Done → Success Metrics → Requirements → Open Questions
- Always ground feature decisions in one of our personas: Jennifer, David, or Rachel
- When I ask for research, give me structured output I can paste into Notion
- When I ask about competitors, only use our known competitive landscape — don't invent new competitors
- Flag when something conflicts with our north star metrics
- When uncertain about our product details, ask me — don't hallucinate LegalGraph features

For competitive analysis:
- Only use known competitors in our space
- Structure as: Product Capabilities → Pricing → GTM → Strengths/Weaknesses
- Always end with "Where LegalGraph Wins" and "Where We're Vulnerable"

For roadmap & prioritization work:
- Always tie recommendations back to our activation rate or AI accuracy metrics
- Surface trade-offs explicitly
```

![alt text](./images/1.5.png)

> **What happens:** Claude reads your four context files, generates the Working Instructions section, and appends it to the existing `./CLAUDE.md`. The file now has both sections — Company & Product from Step 2, and Working Instructions from this step.


---

## What Your Full Setup Looks Like

After completing all three steps, you have two files doing two different jobs.

**`~/.claude/CLAUDE.md` — global, always loaded**

```markdown
# My PM Working Style

- Senior PM — skip the basics, get to the point
- When uncertain, ask — don't guess
- Default PRD template: Problem Statement → User Persona → JTBD → Success Metrics → Requirements → Open Questions
- Default prioritization: RICE scoring
- Always surface trade-offs explicitly
- End all research with "Open Questions"
```

**`./CLAUDE.md` — project, loaded when you're in this folder**

```markdown
## Company & Product

**LegalGraph** — AI-powered contract review for in-house legal teams
...company, product, metrics, personas...

## Working Instructions
...LegalGraph-specific rules, competitor list, persona references...
```

**When you open Claude Code in your LegalGraph folder:**

```
Session starts
    ↓
Claude loads ~/.claude/CLAUDE.md     ← your working style, always
    ↓
Claude loads ./CLAUDE.md             ← LegalGraph context, this project only
    ↓
Both in context — every session
```

Claude doesn't pick one. It reads both. You get your personal style plus the company context — without doing anything.



> **The rule:** Global CLAUDE.md = you. Project CLAUDE.md = the company. Build global first, then layer the company on top.

---

## Your Action Items

1. **Run the global prompt** — build your `~/.claude/CLAUDE.md` with your PM working style
2. **Add your project folder to the chat** — so Claude can see your four context files
3. **Run the Company & Product prompt** — generates the first section of your `./CLAUDE.md`
4. **Run the Working Instructions prompt** — adds the behavioral layer to your `./CLAUDE.md`
5. **Test it** — open a new Claude Code session in your project folder and ask: *"What do you know about me and this project?"* Claude should describe both your working style and LegalGraph

---


*Next: [Module 2 — Commands, Context & Market Research](../Module-2%20-%20Commands%2C%20Context%20%26%20Market%20Research/README.md)*
