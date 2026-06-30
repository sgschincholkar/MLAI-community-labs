# Week 3: Give Your Agent Memory 

Welcome to Week 3 of the AI PM Certification.

In Week 2, you built a RAG pipeline that handles real documents and a multi-agent system that analyzes leases with precision. Your agents could retrieve the right information. But they forgot everything the moment the session ended. This week, you fix that — and then you step into the engineering workflow used by every tech team in the world.

The first two labs give your agent persistent memory. The third lab puts you inside a real codebase with Claude Code, GitHub, and a Pull Request of your own.

Work through the labs in order. Each one builds on the last.

---

## The Labs

### [Lab 3.1 — Short-Term Memory: Make Your Agent Remember Within a Session](./Lab-3.1-n8n-shortterm-memory/Readme.md)

Your agents from Week 2 have no memory between messages. Ask "What is my name?" after telling it your name — it has no idea. This lab shows you exactly why that happens, then fixes it by adding Simple Memory to your n8n workflow.

You'll run the agent without memory first to see the failure, then add the memory node and watch the same agent recall your name correctly. You'll also learn what a "session" is and why this type of memory disappears when you refresh the page — which sets up the problem that Lab 3.2 solves.

**Time:** ~20 minutes

---

### [Lab 3.2 — Long-Term Memory: Make Your Agent Remember Across Sessions](./Lab-3.2-n8n-longterm-memory/Readme.md)

Simple Memory clears when the session ends. This lab builds a persistent memory system using Google Docs as a storage layer — so your agent remembers past conversations even after you close the browser and come back days later.

You'll configure Google Cloud credentials, connect the Google Docs API to n8n, wire up two tools (`save_long_term_memory` and `retrieve_long_term_memory`), and write the system prompt that forces the agent to always save and always retrieve before responding. By the end, refreshing the page no longer wipes the agent's context.

**Time:** ~45 minutes

---

### [Lab 3.3 — PM Dev Tools: Run a Real App and Ship a Change via Pull Request](./Lab-3.3-pm-dev-tools/README.md)

This lab is different. No n8n. No workflows. You're going inside a real codebase — the same environment your engineers work in every day.

You'll create a GitHub account, fork a repository, set up GitHub Desktop, install Claude Code, create a branch, run the app live in your browser, direct Claude to make a real UI change in plain English, and open a Pull Request with a proper title and description. Every step mirrors what a PM does when they want to understand, direct, or contribute to a codebase — without writing a single line of code manually.

By the end, you'll have gone from zero to a submitted Pull Request on a live project.

**Time:** ~2–3 hours

---

### [Lab 3.5 — Build a UI Mockup Agent with Claude Code](./Lab-3.5-claude-how-to-create-subagent/lesson1.1-how-to-create-subagent.md)

This lab teaches you how to build a custom Claude Code subagent — a specialized AI assistant that lives inside your project folder and does one job extremely well.

The agent you will build reads a PRD (Product Requirements Document), parses every screen and user flow described in it, and generates complete HTML and CSS mockups for each screen. All mockups are saved in a `/mockups` folder with an `index.html` that links them all together.

You will learn how to use the `/agents` command inside Claude Code, choose the right model (Haiku vs Sonnet vs Opus), configure tool permissions, and set up project-scoped memory — so you understand not just how to build an agent, but why each configuration decision matters.

**Time:** ~45 minutes

---

> If you get stuck in any lab, each one has troubleshooting guidance built in. Read the error carefully — most issues in these labs have a one-line fix.
