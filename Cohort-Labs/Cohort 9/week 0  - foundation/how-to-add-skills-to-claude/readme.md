# Lesson - How to Add Skills to Claude

![claude](./assets/banner.png)

## Overview

Skills are one of the most powerful features in Claude. They let you save reusable prompts as slash commands — so instead of typing the same detailed instructions every session, you run one command and get consistent, structured output every time.

By the end of this lesson you will:

- Install your first skills into Claude
- Understand what skills are and why they matter
- Know when to use a skill vs. a regular prompt
- Know how to create your own custom skills

---

## Starter Skills for This Course

Download and install these five skills to use throughout the program. Each one is built for a core PM workflow — install them in order and you'll have the full discovery-to-delivery stack ready to go.

| # | Skill | Command | What It Does | Download |
|---|---|---|---|---|
| 1 | Idea Eval | `/idea-eval` | Evaluates a product idea across problem severity, market size, feasibility, and business potential | [Download](https://pragyaallc-my.sharepoint.com/:t:/g/personal/sachin_parmar_legalgraph_ai/IQAlA9O4OLqLSrvdEXgpZJ9YAb8uJs38P-Cvc5BI9kwQNv0?e=bWLFDF) |
| 2 | Market Research | `/market-research` | Analyzes a market — size, players, trends, opportunities, and key insights for your team | [Download](https://pragyaallc-my.sharepoint.com/:t:/g/personal/sachin_parmar_legalgraph_ai/IQCwxLJr3-XKTqU_Xo9ktzMlARtfX5VuIeD4dvhfm3adAw8?e=GSBweE) |
| 3 | User Research | `/user-research` | Synthesizes user research input into findings, pain points, and product recommendations | [Download](https://pragyaallc-my.sharepoint.com/:t:/g/personal/sachin_parmar_legalgraph_ai/IQAPNUc3xnVASoPOKxepVkR3Ad9KwoiIbdnYWGBUcVYocuk?e=byQyfS) |
| 4 | Write Your PRD | `/write-your-prd` | Guides you through writing a complete PRD from scratch | [Download](https://pragyaallc-my.sharepoint.com/:t:/g/personal/sachin_parmar_legalgraph_ai/IQARMbe9Qlz1R4yuqWzKKwQoAQlgWsZNLIEnP8z4xposz1Y?e=i7lrrb) |
| 5 | PRD Eval | `/prd-eval` | Reviews a PRD for gaps, ambiguity, missing sections, and readiness to hand to engineering | [Download](https://pragyaallc-my.sharepoint.com/:t:/g/personal/sachin_parmar_legalgraph_ai/IQBs7yXfTt-xS7O9pGHlFavGAYhL8cn-iO6Ctdi5UO5Z8ws?e=xNQdZ4) |

**Want to go deeper?** Read the [Complete Guide to Building Skills for Claude](https://resources.anthropic.com/hubfs/The-Complete-Guide-to-Building-Skill-for-Claude.pdf) for a full walkthrough from Anthropic.

---

## How to Install Skills in Claude

### Step 1: Open Claude

Open Claude . You can start from any surface — **Cowork**, or **Code**.

> **Don't have Claude set up yet?**
> Complete [Lesson 1.0 — Installation & Claude Overview](../lesson-1-claude-code-setup/Lesson1.0%20-%20Installation.md) first, then come back here.

---

### Step 2: Go to Cowork and Open Customize

1. In the left sidebar, click **Cowork**
2. Once inside Cowork, click the **Customize** section

![claude](./assets/1.png)

---

### Step 3: Open Skills and Add a New Skill

1. Click **Skills**
2. Click **Add**
3. Select **Create Skill**
4. Choose **Upload Skill**

![claude](./assets/2.png)

---

### Step 4: Upload the Skill File

1. Select the skill file you downloaded (e.g. `market-research.md`)
2. Confirm the upload

Repeat Steps 3–4 for each of the five skill files.

![claude](./assets/3.png)


---

### Step 5: Confirm Installation

Once installed, your skills will appear under **Personal Skills**. You can now invoke any of them from a Cowork session by typing the slash command — for example:

```
/market-research AI-powered contract review tools
```

![claude](./assets/4.png)

![claude](./assets/5.png)

---

## What Are Skills?

A **skill** is a saved prompt you can trigger with a slash command like `/market-research` or `/prd-eval`. When you run a skill, Claude follows the instructions you defined — every time, in the same format.

Think of skills as your personal playbook. Instead of re-explaining how you want a PRD reviewed or a user interview analyzed, you write those instructions once, save them as a skill, and invoke them instantly from any session.

---

## Why Skills Matter for PMs

| Without Skills | With Skills |
|---|---|
| Re-type the same prompt every session | One command, every time |
| Inconsistent output format | Structured, predictable results |
| Prompts lost between conversations | Saved permanently to your profile |
| Hard to share with teammates | Skills can be shared and standardized |

Skills turn your best prompts into repeatable workflows. Every time you find yourself typing the same thing twice, that's a skill waiting to be created.

---

## When to Use a Skill

Use a skill when:

- You run the same type of analysis repeatedly (market research, user interviews, PRD reviews)
- You need output in a specific, consistent structure every time
- You want to share a prompt workflow with your team
- You're building a repeatable process into your workflow

Use a regular prompt when:

- It's a one-off question or task
- The context changes too much each time to generalize
- You're exploring or experimenting

---

## How to Create Your Own Skills

Once you've used the starter skills, you can build your own. A skill is just a Markdown file with instructions — the filename becomes the slash command.

**To create a skill from scratch:**

1. Open a text editor (or ask Claude to help you write it)
2. Write the instructions you want Claude to follow — be explicit about the output format you want
3. Save the file as `your-skill-name.md`
4. Follow Steps 2–4 above to upload it

**Tips for writing effective skills:**

| Tip | Why It Matters |
|---|---|
| Be explicit about output format | Claude will follow structure instructions precisely |
| Use `$ARGUMENTS` as a placeholder | Anything you type after the command replaces `$ARGUMENTS` — makes skills dynamic |
| Keep each skill focused on one job | Narrow skills are more reliable than multi-purpose ones |
| Add a constraints or out-of-scope section | Prevents Claude from over-generating or going off-track |

**Example — a simple skill file:**

```
Write a user story for the following feature: $ARGUMENTS

Format:
**User Story**
As a [user], I want [goal] so that [benefit].

**Acceptance Criteria**
- [ ] Criterion 1
- [ ] Criterion 2

**Out of Scope**
- What this story does not cover
```

Save this as `write-user-story.md`, upload it, and invoke it with:

```
/write-user-story Export project data as a CSV
```

---

## Summary

| What You Learned | Key Takeaway |
|---|---|
| What skills are | Saved prompts you trigger with a slash command |
| Why they matter | Consistent output, no re-typing, shareable across your team |
| When to use them | Anytime you run the same type of task more than once |
| How to install | Cowork → Customize → Skills → Add → Upload |
| How to create your own | Write a `.md` file with instructions and upload it |

Skills are one of the highest-leverage habits you can build as an AI-powered PM. Start with the four starter skills, then build your own as you find prompts worth keeping.
