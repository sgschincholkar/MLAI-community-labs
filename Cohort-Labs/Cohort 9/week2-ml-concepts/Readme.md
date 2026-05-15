# Week 2: Make Your Agent Handle Real Documents

![banner](./assets/1.png)

Welcome to Week 2 of the AI PM Certification.

In Week 1, you built a working AI agent. It read a contract, answered questions, and felt like something real. This week, you find out why that agent breaks on real documents — and you build the architecture that fixes it.

The fix is called RAG. By the end of this week, you'll understand it well enough to build it, explain it to a stakeholder, and extend it into a system that handles complex analysis no single AI call could do alone.

Each lab builds directly on the last. Work through them in order. By the end, you'll have gone from a broken agent to a multi-agent lease analysis system — and you'll know exactly why every piece is there.

No prior ML experience needed. Just the n8n account and OpenAI key from Week 1.

---

## The Labs

### [Lab 1.1 — Why Your Agent Breaks on Real Contracts](./1.1-why-we-need-RAG/Readme.md)

Before you fix anything, you need to see what's actually broken. You'll take the agent from Week 1 and run it on a large contract — one that's closer to what real documents look like. It either fails outright or gives you a degraded answer. Either way, you'll understand exactly why.

This lab is short. It's a diagnostic, not a build. But it sets up everything that follows — once you see the failure mode, the solution in Lab 1.2 will make complete sense.

**Time:** ~15 minutes

---

### [Lab 1.2 — Build Your First RAG Pipeline](./1.2-understanding-RAG/Readme.md)

This is where you build the fix. You'll create a two-workflow system: one that ingests a large contract and breaks it into searchable chunks, and one that retrieves exactly the right chunk when a user asks a question — without hitting context limits.

Along the way, you'll learn what embeddings actually are, why chunk size and overlap matter, what the Recursive Text Splitter does differently, and how to configure a vector store that actually works on PDF documents. By the end, you'll have a live contract Q&A system that handles large files correctly.

**Time:** ~40 minutes

---

### [Lab 1.3 — Agentic RAG: When One Retriever Isn't Enough](./1.3-agentic-RAG/Readme.md)

Basic RAG works for simple questions. It breaks on complex ones. Ask "Is this lease safe to sign?" and a single retriever dumps five chunks on one AI — which has to simultaneously plan, retrieve, analyze risk, extract timelines, and write a coherent answer. It misses things.

This lab fixes that with a multi-agent system built specifically for lease contracts. A planning agent figures out what to search for. An orchestrator runs targeted retrieval and routes the results. Two specialist agents — one for risk, one for obligations — each do one job and do it well. The output is structured, deep, and sourced from actual clause evidence.

**Time:** ~50 minutes

---

### [Lab 1.4 — Run the Full PM Loop with Claude Skills](./1.4-claude-skills/Readme.md)

Now you step back into the PM role. You've built the technical system — now use it as the foundation for a product idea. In this lab, you'll run the full discovery-to-specification process on a Compliance Lease Tool using four Claude Skills: market research, user research, PRD writing, and PRD evaluation.

Each skill is a slash command that runs a structured framework and saves a document to your project workspace. By the end, you'll have four connected documents — market landscape, user evidence, product spec, and reviewed spec — that tell the full story of a product from idea to ready-to-build.

**Time:** ~30 minutes

---

> If you get stuck in any lab, each one has troubleshooting guidance built in. Read the error carefully — most issues in these labs have a one-line fix.
