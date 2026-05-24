# Lab 1.2: Build Your First Prototype with Claude Code

![banner](./assets/op.png)

You just built an AI agent in n8n. Now you're going to build the actual web app that sits in front of it — using Claude Code to write all the code.

But here's what's different about this lab. We're not going to explain everything upfront. We're going to build first. And somewhere in the middle, something's going to feel slightly off — and that friction is exactly the point.

By the end of this lab, you will have a working contract review web app. You'll understand what CLAUDE.md is — and more importantly, *feel* why it exists. You'll know how to go from a single prompt to a testable prototype in one session. And you'll finally understand the difference between Claude Chat, Claude Cowork, and Claude Code.

No coding experience needed. Just the Claude app and about 30 minutes.

---

## What Are We Building?

A **Contract Review Web App** — the same use case from Lab 1.1, now as a real interface.

A user opens the app, uploads a contract PDF, types a question in the chat panel, and gets a response. For now the responses are simulated — we'll wire up the real AI in Lab 1.3. The goal of this lab is to build the shell: something that works, looks like a real product, and is ready to connect.

---

## Before You Build: Pick the Right Claude

Claude isn't one thing. There are three modes, and using the wrong one caps what's possible.

![banner](./assets/2.png)

**Claude Chat** is for thinking. Ask, iterate, reason through a problem. No file access, no autonomy — just conversation. Great for brainstorming. The trap is staying here when you need to actually produce something.

**Claude Cowork** is for doing. Describe a task and it executes autonomously — creates Word docs, slide decks, PDFs, spreadsheets. Connects to Gmail, GitHub, Slack. Good for non-technical users who want output without a terminal.

**Claude Code** is for building. It lives in your terminal, reads and writes your actual files, runs your tests, sees errors in real time, knows your git state. Every action is visible and traceable. This is where builders work.

This lab uses Claude Code.

> ✓ A simple decision rule: does this involve code or files? Go to Code. Want a doc or report automated? Go to Cowork. Still figuring out what you want? Start in Chat.

---

## Prerequisites

✅ The **Claude desktop app** — [download here](https://claude.ai/download). New to Claude Code? [Follow this setup guide](../../week%200%20%20-%20foundation/lesson-1-claude-code-setup/Lesson1.0%20-%20Installation.md) to get it running in under 5 minutes.

✅ **Claude Code** — built into the Claude desktop app, no extra install needed.

✅ The **sample contract PDF** from Lab 1.1 — same file, use it again here. [Download it here](https://pragyaallc-my.sharepoint.com/:b:/g/personal/sachin_parmar_legalgraph_ai/IQC2WQJhhIuyRq5JrVY13FwNAdwS4M5gB5w-qzBAm9V4mRQ?e=XyvLU4) if you don't have it.

✅ The **CLAUDE.md template** — you'll use this in Part 3 and Part 4. [Download it here](https://pragyaallc-my.sharepoint.com/:t:/g/personal/sachin_parmar_legalgraph_ai/IQB4LEMKjmINRqRJCcYJ3HRoAVQwmLvrF3QwHfBj2Ioon5w?e=VqcxG0). 

---

## Part 1: Build First, Ask Questions Later

Let's start with action. No theory, no setup rituals — just build.

Open the Claude desktop app. If you haven't installed it yet, go to claude.ai/download, install it for your OS, and sign in with your Claude account.

![flow](./assets/11.png)

Once you're in, find **Claude Code** in the sidebar and click it. You'll land in a terminal-style interface — this is Claude working directly in your file system, not a chat window. It feels different from the chat you're used to. That's intentional. This is the building environment.

![flow](./assets/1.png)

Next, create a new folder on your Desktop called `contract-review-app` and point Claude Code at it using the folder picker. Everything Claude builds will land here.

![flow](./assets/4.png)

Now — don't overthink this next part. Just run this prompt exactly as written:

```
Build a contract review web app.

The app should have:
- A file upload area where users can upload a PDF contract
- A chat panel where users can type questions and see responses
- When the user types anything and hits send, respond with:
  "This is a simulated response. AI integration coming soon."
- A clean two-column layout: contract on the left, chat on the right

Create all files in the current directory using plain HTML, CSS, and JavaScript.
No frameworks, no npm, no build tools. Just files I can open in a browser.
```

Watch Claude work. It'll generate `index.html`, `style.css`, and `script.js` in your folder.

![flow](./assets/12.png)

When it's done, go to your `contract-review-app` folder and open the app:

**On Mac:** Open Finder → Desktop → contract-review-app → right-click `index.html` → Open With → your browser

**On Windows:** Open File Explorer → Desktop → contract-review-app → double-click `index.html`

You should see the app load in a new browser tab.

![flow](./assets/14.png)

Try it. Upload the sample contract PDF. Type *"What is this contract about?"* and hit send. Type *"What are the payment terms?"* You'll get the same dummy response every time — that's expected. The AI isn't connected yet. What we're testing is the structure: does the upload work, does the chat work, do both panels show up?

If yes — the shell is working. Move on.

---

## Part 2: The Thing That's Missing

Take a moment and really look at what Claude built.

It works. The upload button takes a file. The chat takes a message and replies. The two-column layout is there.

But be honest with yourself. Does it look like something *your team* would ship? Does it use your brand colors? Your preferred font? The spacing and visual style your design system follows?

Probably not.

Claude made decisions on your behalf. It picked a font, chose some colors, set a spacing rhythm — and they're fine. They're just not *yours*. And here's the thing that will start to bother you after a few sessions: tomorrow, if you open a new project and run a similar prompt, Claude will make completely different decisions again. It has no memory of what you showed it today. Every session starts from zero. You'd have to describe your preferences all over again, and the week after that, and every time after that.

This is the friction that quietly kills momentum for most people who start building with AI tools.

There should be a way to teach Claude how you build — once — and have it remember.

There is.

---

## Part 3: Meet CLAUDE.md

When Claude Code opens a project folder, the very first thing it does is look for a file called `CLAUDE.md`. If it finds one, it reads it before touching anything else.

This file is **Claude's operating system for your project.**

It's not a config file. It's not documentation. It's a briefing — the same way you'd brief a new team member before their first day. You write it once, and Claude reads it at the start of every single session. Everything in that file becomes the default. Font choices, color values, code conventions, design philosophy — whatever you put in there, Claude follows. Without you having to say it again.

![banner](./assets/3.png)

Think of it this way: without CLAUDE.md, Claude starts every session as a blank slate. With it, Claude already knows how your team builds.

There are actually three places you can put a CLAUDE.md file, depending on who you want to share it with:

| File | Location | Shared with team? | What it's for |
|---|---|---|---|
| `CLAUDE.md` | Project root | ✅ Yes — committed to git | Project-wide instructions for everyone |
| `CLAUDE.local.md` | Project root | ❌ No — in `.gitignore` | Your personal preferences, stays off the shared repo |
| `CLAUDE.md` | `~/.claude/` | ❌ No — your machine only | Global instructions across every project you work on |

For this lab, we'll work at two levels — global first, then project.

**Set up the global CLAUDE.md first:**

1. Open the Claude desktop app and go to **Claude Code**
2. Attach the `CLAUDE.md` template file you downloaded from the prerequisites section
3. Run this prompt:

```
Use this CLAUDE.md file as my global Claude configuration. Save it to ~/.claude/CLAUDE.md so it applies across every project I work on.
```

This tells Claude your defaults once — and they carry into every future project automatically, not just this one.

Now we'll also set one up at the project level, which is what the next part covers.

---

## Part 4: Set It Up and Run It Again

Now set up the **project-level** CLAUDE.md. This one lives inside your `contract-review-app` folder and shapes only this project — committed to git so your whole team gets it.

Here's the difference between the two levels:

| Level | File location | Who it applies to | Committed to git? |
|---|---|---|---|
| **Global** | `~/.claude/CLAUDE.md` | You, across every project | No — stays on your machine |
| **Project** | `contract-review-app/CLAUDE.md` | Everyone working on this project | Yes — shared with the team |

You already set the global one in Part 3. Now create the project-level one.

> This template is a starting point — update it with your own company name, brand colors, and design conventions before using it in a real project.

Run this in Claude Code:

```
Create a CLAUDE.md file in this folder with the following content:

# Contract Review App

A web-based contract review prototype built for the AI PM Certification course.

## What This Is
An app where users upload a contract PDF and ask questions about it in a chat interface.

## Tech Stack
- Plain HTML, CSS, and vanilla JavaScript
- No frameworks, no build tools, no npm
- Single folder, runnable by opening index.html in a browser

## Design Rules
- Font: Inter (import from Google Fonts)
- Brand colors: #0F172A (dark navy) for headers, #F97316 (orange) for buttons and accents
- Background: #F8FAFC (light gray), not white
- Design style: clean, minimal, professional — like a real SaaS product
- Two-column layout: contract viewer left, chat panel right
- Generous padding, clear visual hierarchy, no clutter

## Code Rules
- Keep code simple and readable
- Modular structure — separate concerns across files
- No external libraries unless absolutely necessary
```

Once Claude creates it, open the file and read it. This is now your project's source of truth — the standing brief Claude will follow for every change, every iteration, every session from this point forward.

![flow](./assets/15.png)

![flow](./assets/6.png)

Now here's the experiment. Run the exact same prompt you used in Part 1. Word for word, nothing changed:

```
Build a contract review web app.

The app should have:
- A file upload area where users can upload a PDF contract
- A chat panel where users can type questions and see responses
- When the user types anything and hits send, respond with:
  "This is a simulated response. AI integration coming soon."
- A clean two-column layout: contract on the left, chat on the right

Create all files in the current directory using plain HTML, CSS, and JavaScript.
No frameworks, no npm, no build tools. Just files I can open in a browser.
```

![flow](./assets/16.png)

Refresh your browser when Claude finishes. Then look at what you have.

The prompt didn't change. But the output did.

Inter font. Orange buttons. Dark navy headers. Light gray background. The spacing feels considered. It looks like something you'd actually put in front of a stakeholder.

> *Claude didn't become smarter. It became aligned with how you work.*

That's the aha moment. The intelligence didn't change — the context did. And context is everything.

![flow](./assets/17.png)

---

## Part 5: One More Iteration

The structure is solid and the style is aligned. Now let's improve two things: the visual finish and a contract preview panel so users can read the document while they chat.

Run this in Claude Code:

```
Improve the prototype with two changes:

1. UI polish — refine the interface to feel more like a production-ready product.
   Better spacing, visual hierarchy, and polish throughout.

2. Contract preview — when the user uploads a PDF, display the contract
   in the left panel so they can read it while asking questions in the chat.
   Both panels should be visible and independently scrollable.
```

Refresh the browser when Claude finishes and test it end to end. Upload the sample contract — it should appear in the left panel. Type a question in the chat — you get the simulated response back. Try scrolling both panels independently.

> ★ A prototype with dummy responses is still a prototype. You can show this to a stakeholder right now, get feedback on the layout, and validate the concept — before connecting a single line of real AI logic. Shell first. Intelligence second.

If the contract doesn't show up in the left panel after uploading, just describe it to Claude: *"The PDF isn't rendering in the left panel — the chat still works but the preview is blank."* One message is usually enough to fix it.

---

## What You Learned

You started this lab by just building — no setup, no context, no rules. Claude made decisions for you, and the result worked but felt generic. Then you felt the friction of having to repeat yourself. Then you discovered the fix.

**CLAUDE.md is the file where you teach Claude how your team builds.** Write it once. It runs before every session. Fonts, colors, conventions, design style — it all becomes Claude's default. The brief you never have to repeat.

**Same prompt, different output.** The demonstration is the point. CLAUDE.md doesn't change the prompt — it changes what Claude already knows when it reads the prompt. Context is everything.

**Three modes, three jobs.** Chat for thinking. Cowork for doing. Code for building. Using the right one isn't just about speed — it's about what's even possible.

**Iteration-first prototyping.** Structure first, polish second, AI integration third. Trying to do all three at once is how prototypes stall.

---

## What's Next

In the next lab, you'll connect this prototype to the n8n agent from Lab 1.1. The dummy responses go away — replaced by your live contract review agent, wired directly into this UI.

Two labs. One working product.

---

[→ Continue to Lab 1.3: Connect Your n8n Agent to Your Prototype](../1.3%20-%20connect-n8n-prototype/readme.md)
