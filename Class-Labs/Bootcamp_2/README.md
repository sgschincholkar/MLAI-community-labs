# AI PM Interview Bootcamp — Claude Code for Product Managers

![images](./images/image.png)

Learn how to use Claude Code as a full PM operating system — from setting up your context and running research, to building prototypes, connecting external tools, and automating your workflow.

---

## Who This Is For

Product Managers who want to move faster, produce better research, and spend less time on mechanical PM work — using Claude Code as a configured workflow system, not just a chat tool.

No coding background required. Every lesson is built for PMs.

---

## Modules

### [Module 1 — Claude Foundation](./Module-1%20-%20ClaudeFoundation/README.md)
**Get set up and understand how Claude thinks**

Before you can use Claude Code effectively, you need to understand how it loads context and how to make that context persistent. This module covers installation, the interface, and — most importantly — building your `CLAUDE.md` files so Claude knows who you are, how you work, and what product you're building.

| Lesson | Topic |
|--------|-------|
| [1.0 — Installation](./Module-1%20-%20ClaudeFoundation/Lesson1.0%20-%20Installation.md) | Install Claude Code and set up your environment |
| [1.1 — Download the Project Repository](./Module-1%20-%20ClaudeFoundation/Lesson1.1-understand-the-interface.md) | Download the bootcamp workspace — the folder where all your outputs will live |
| [1.2 — Understanding Context](./Module-1%20-%20ClaudeFoundation/Lesson1.2-Understanding-Context.md) | How Claude uses context and why it matters for every prompt you run |
| [1.3 — CLAUDE.md: Your PM Brain](./Module-1%20-%20ClaudeFoundation/Lesson1.3-CLAUDE.md-your_PM_brain.md) | Build your global working style file and your project company context file |

**What you'll have:** Claude Code installed, your workspace set up, and CLAUDE.md loaded with your PM working style and LegalGraph company context — so every future session starts with Claude already briefed.

---

### [Module 2 — Commands, Context & Research](./Module-2%20-%20Commands%2C%20Context%20%26%20Market%20Research/README.md)
**Build a reusable PM command library and run a full research-to-PRD workflow**

This module is where Claude Code becomes a real PM tool. You build three reusable slash commands, then use them to run a full chained research workflow — market research, user research, and a structured PRD — all on the same feature (Lease Compliance Reporting for LegalGraph). Every lesson builds on the output of the last.

| Lesson | Topic |
|--------|-------|
| [2.1 — Slash Commands](./Module-2%20-%20Commands%2C%20Context%20%26%20Market%20Research/Lesson2.1-Slash-Commands-in-Claude-Code.md) | How built-in and custom slash commands work in Claude Code |
| [2.2 — Custom Slash Commands](./Module-2%20-%20Commands%2C%20Context%20%26%20Market%20Research/Lesson2.2-Custom-Slash-Commands.md) | Build `/market-research`, `/user-research`, and `/prd` — reusable for any feature, any project |
| [2.3 — Market Research](./Module-2%20-%20Commands%2C%20Context%20%26%20Market%20Research/Lesson2.3-Chaining-Research-Prompts.md) | Chain 4 research stages on Lease Compliance — market size, competitors, customer pain points, full synthesis |
| [2.4 — User Research](./Module-2%20-%20Commands%2C%20Context%20%26%20Market%20Research/Lesson2.4-User-Research-Chaining.md) | Chain user research using the market research as context — personas, workflow, ranked pain points |
| [2.5 — PRD](./Module-2%20-%20Commands%2C%20Context%20%26%20Market%20Research/Lesson2.5-PRD.md) | Turn both research outputs into a structured PRD — requirements, success metrics, open questions |

**What you'll have:** Three slash commands in your personal library. Three output files saved in `outputs/`. CLAUDE.md updated with market intelligence, user insights, and PRD decisions — loading automatically every session.

---

### [Module 3 — Prototype, Connector & Automate](./Module-3%20-%20Prototype%2C%20Connect%20%26%20Automate/README.md)
**Turn your PRD into a prototype, connect Claude to your tools, and automate your PM workflow**

Module 3 picks up directly from the PRD you built in Module 2. You generate a clickable prototype from it, connect Claude to external tools like Notion and Jira via MCP connectors, and set up skills and hooks that automate quality checks and recurring PM tasks — without you having to remember to run them.

| Lesson | Topic |
|--------|-------|
| [3.1 — Creating Mocks and Deploying](./Module-3%20-%20Prototype%2C%20Connect%20%26%20Automate/Lesson3.1-Creating-Mocks-and-Deploying.md) | Generate a clickable HTML prototype from your PRD and deploy it via Tiiny.host in 30 seconds |
| [3.2 — CoWork: Job Assistants and Connectors](./Module-3%20-%20Prototype%2C%20Connect%20%26%20Automate/Lesson3.2-CoWork:%20Creating-a-Job-Assistant-and-Understanding-Connectors.md) | Build `/standup` and `/competitive-intel` job assistants, connect Claude to Notion via MCP |
| [3.3 — Skills and Hooks](./Module-3%20-%20Prototype%2C%20Connect%20%26%20Automate/Lesson3.3-Skills-and-Hooks.md) | Create reusable PM skills for automatic PRD review, and hooks that run without prompting |

**What you'll have:** A deployed clickable prototype. Job assistants that handle recurring PM tasks. A Notion connector that saves research outputs directly to your workspace. Skills and hooks that enforce quality standards automatically.

---

## The Full Workflow

Every lesson across all three modules works on the same feature — **Lease Compliance Reporting for LegalGraph**. By the end you'll have built this chain from scratch:

```
Module 1
CLAUDE.md (working style + company context) → loads every session
        ↓
Module 2
/market-research → outputs/market-research-lease-compliance-<date>.md
/user-research   → outputs/user-research-lease-compliance-<date>.md
/prd             → outputs/prd-lease-compliance-<date>.md
        ↓
Module 3
PRD → mocks/lease-compliance-prototype.html → deployed on Tiiny.host
Job assistants → /standup, /competitive-intel
Skills & Hooks → PRD review, session greeter, research tone guard
```

Each output feeds the next. Each module builds on the last.

---

## Prerequisites

- A computer running Mac or Windows
- A Claude account (claude.ai) — Pro or Max plan recommended
- No coding experience required

---

*Start here: [Module 1 — Claude Foundation](./Module-1%20-%20ClaudeFoundation/README.md)*
