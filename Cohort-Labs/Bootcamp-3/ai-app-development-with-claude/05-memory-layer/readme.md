[← Lesson 4](../04-building-the-application/readme.md) | **Lesson 5**

---

# Lesson 5 — Memory Layer

## Where We Are

By this point you have:

- **Lesson 1** — Forked the `dev-os` starter repo, cloned it to your machine, and opened it in VS Code.
- **Lesson 2** — Explored the five skills and reviewed the design system in `docs/design.md`.
- **Lesson 3** — Used Plan Mode to run `/engineering-planner` and `/implementation-specs`, producing the engineering documents in `docs/engineering/`.
- **Lesson 4** — Scaffolded the Next.js project, implemented the application, ran the database schema in Supabase, and confirmed the app loads in a browser.

Now you are going to give the assistant a memory. Currently every time a user sends a message, a new session is created — the assistant has no idea what was said before, what contract was uploaded, or what questions were already asked. This lesson fixes that.

---

## The Problem — No Memory

Open your running app and go to the chat interface. Ask the assistant something about the contract:

```
What is the termination clause?
```

It answers correctly. Now ask a follow-up:

```
Can you summarise what you just told me?
```

The assistant has no idea what it just told you. It cannot answer the follow-up because each message is a brand new, isolated API call with no context carried over.

This is the problem memory solves.

---

## What Is Memory in an AI Application?

Memory is not a single thing — there are four distinct types, and it is important to know which one you are using and why.

| Type | Where It Lives | How Long It Lasts | Example |
|---|---|---|---|
| **In-Context Memory** | The `messages[]` array sent to the API | Current session only | Passing the last 10 chat turns to the model |
| **External / Persistent Memory** | A database (Supabase) | Forever, until deleted | Saving every message to `chat_messages` and reloading it next visit |
| **Retrieved Memory (RAG)** | A vector store or semantic search index | Forever | Searching across all past contracts to find relevant clauses |
| **Parametric Memory** | Baked into the model's weights at training time | Permanent — you cannot change it without retraining | General legal knowledge the model already has |

### What We Are Building in This Lesson

We are combining **In-Context Memory** with **External / Persistent Memory**:

```
User sends a message
        │
        ▼
Fetch all previous messages for this session from Supabase
        │
        ▼
Classify the question — does it refer to:
  → Contract content only
  → Conversation history only
  → Both
        │
        ▼
Build the context window:
  [system prompt] + [contract text if needed] + [message history] + [new question]
        │
        ▼
Send to Claude API
        │
        ▼
Save the new user message + assistant response back to Supabase
        │
        ▼
Return the response with source attribution
```

The external memory (Supabase) is what makes history survive a page refresh. The in-context memory is what makes follow-up questions work within a session.

---

## Before vs After

**Before this lesson:**

```
Turn 1: "What is the termination clause?"  →  API call (contract text only)
Turn 2: "Summarise what you just said"     →  API call (nothing — starts fresh)
                                                ↑ BROKEN
```

**After this lesson:**

```
Turn 1: "What is the termination clause?"  →  API call (contract text)
                                           ←  Answer saved to Supabase
Turn 2: "Summarise what you just said"     →  API call (contract text + Turn 1 + Turn 2)
                                           ←  Works — AI remembers Turn 1
```

---

## Step 1 — Open a Claude Code Session

Open a terminal in VS Code and navigate to your project folder. Start Claude Code:

```bash
claude
```

---

## Step 2 — Run the Memory Layer Prompt

Copy and paste the following prompt into the Claude Code session:

```
Implement a Conversation Memory Layer.

Currently, the chatbot does not have access to previous messages because a new session is created for each interaction. The assistant should have access to:
- Uploaded contract/document
- Current chat session history
- Previous user questions
- Previous assistant responses

Before generating a response, the system must determine whether the user's question refers to:
- Contract content
- Conversation history
- Both contract content and conversation history

Based on this classification, the assistant should retrieve the appropriate context and generate an accurate response with proper source attribution.
```

Press **Enter**.

---

## What This Prompt Does

The prompt instructs Claude to make three targeted changes to the existing chat implementation:

**1. Load history before every response**
Before calling the Claude API, the chat route now fetches all previous messages for the current session from the `chat_messages` table in Supabase. These are passed to the API as the `messages[]` array so the model sees the full conversation.

**2. Add a query classifier**
A lightweight classification step runs on the user's question before the API call. It categorises the question into one of three buckets:

| Classification | Context Included |
|---|---|
| `contract` | System prompt + contract text only |
| `history` | System prompt + message history only |
| `both` | System prompt + contract text + message history |

This keeps the context window lean — a question like "what did you say earlier?" does not need the full contract text, and a question about a specific clause does not need a long chat history.

**3. Save messages and add source attribution**
Every user message and every assistant response is saved to `chat_messages` immediately. Responses include a `[Page X]` citation so the user can trace the answer back to the contract.

---

## What Claude Will Change

Claude will modify the existing chat API route and may create a small helper module. The changes are surgical — the rest of the application is untouched.

Files typically modified:

```
app/
└── api/
    └── chat/
        └── route.ts          ← main changes here

lib/
└── memory/
    └── index.ts              ← new: loads history, classifies query, saves messages
```

Review the diff before approving. Confirm that:

- The existing upload and extraction flows are unchanged
- The `chat_messages` table write happens after every turn, not just on success
- The classifier falls back to `both` when the query type is ambiguous

---

## Step 3 — Test the Memory

Start the development server if it is not already running:

```bash
npm run dev
```

Open the app and go to the chat interface for any previously uploaded contract. Run through this test sequence:

| Turn | Message | What to Check |
|---|---|---|
| 1 | Ask about a specific clause (e.g. "What is the governing law?") | Answer is grounded in the contract, includes a page citation |
| 2 | Ask a follow-up ("What does that mean in practice?") | AI references its own previous answer — memory is working |
| 3 | Refresh the page and reopen the same contract | Chat history reloads from Supabase — persistence is working |
| 4 | Ask "What have I asked you so far?" | AI summarises the conversation — history retrieval is working |

If Turn 3 fails (history does not reload), check that the `chat_messages` Supabase write is completing without error. Open the browser dev console and look for a failed fetch.

---

## What You Have Built

At the end of this lesson your application has:

- **In-context memory** — the full conversation history is passed to the model on every turn, enabling follow-up questions and multi-turn reasoning
- **Persistent memory** — every message is saved to Supabase so history survives page refreshes and return visits
- **Query classification** — the system only includes the context the question actually needs, keeping API calls efficient
- **Source attribution** — every response cites the page it drew from, so users can verify answers against the original document

---

## What You Learned

- **The four types of AI memory** — in-context (messages array), external/persistent (database), retrieved (RAG/vector search), and parametric (baked into model weights) — and why this lesson combines the first two to solve the stateless API problem.
- **Why stateless calls break multi-turn chat** — each API call starts fresh with no knowledge of previous turns; persisting messages to Supabase and reloading them before every call is what makes follow-up questions work.
- **Query classification for lean context windows** — categorising each question as `contract`, `history`, or `both` before calling the API means the model only receives the context it actually needs, keeping calls fast and cost-efficient.
- **The memory data flow** — fetch history from Supabase → classify query → build context window → call Claude API → save user message and assistant response; this loop runs on every turn.
- **How to verify memory is working** — the four-turn test sequence (specific question, follow-up, page refresh, history summary) confirms in-context memory, persistent storage, and history retrieval independently.
- **Source attribution as a trust mechanism** — citing the exact page the answer came from lets users verify the AI's reading against the original document, which is critical in a legal context where a misread clause has real consequences.

---

[← Lesson 4](../04-building-the-application/readme.md) | **Lesson 5**