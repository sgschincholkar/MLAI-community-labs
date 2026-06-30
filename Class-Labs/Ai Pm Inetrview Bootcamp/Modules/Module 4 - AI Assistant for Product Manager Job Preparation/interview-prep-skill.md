---
name: interview-prep
description: Full-stack PM interview preparation skill. Use this when a user wants to prepare for a Product Manager interview — any round, any company, any level. Collects resume and job description via AskUserQuestion, then generates personalized prep files: 5 STAR stories, project discussion points, interview strategy, and deep-dive round 2 prep including case studies, behavioral questions, and strategic questions to ask interviewers.
---

## Context

Reference this file for the full workflow, prompts, and strategy framework this skill is based on:

@"Bonus - 4.5-how-to-build-strategy-using-claude-code.md"

---

## Goal

This skill creates a personalized job interview preparation package for Product Manager roles. It handles both **Round 1** (first screening call) and **Round 2** (panel / deep dive) preparation by generating tailored, file-based prep materials from your resume and job description.

---

## Behavior

Trigger this skill when a user says:
- "prepare me for my interview"
- "interview prep"
- "get me ready for my first call"
- "prep for round 2"
- "job interview strategy"
- Anything about PM interview preparation for a specific role or company

---

## Phase 1 — Intake

Use the `AskUserQuestion` tool to collect inputs before generating anything.

**Step 1 — Round Selection**

Ask which interview round they are preparing for:
- **Round 1:** First Screening / Recruiter Call
- **Round 2:** Panel / Hiring Manager / Deep Dive
- **Full Prep:** Both rounds — complete package

**Step 2 — Resume**

Ask the user to provide their resume. Accept either:
- Pasted text
- A file reference using `@filename.pdf`

**Step 3 — Job Description**

Ask the user to paste the full job description text.

**Step 4 — Round 2 Context (Round 2 or Full Prep only)**

If the user selected Round 2 or Full Prep, additionally ask:
- What questions or topics came up in Round 1 (if they had it)
- Who they are meeting: Hiring Manager, peer PM, tech lead, skip-level, etc.

**CRITICAL RULE:** Do NOT generate any output until BOTH resume and job description are provided. Keep asking until you have both.

---

## Phase 2 — Round 1 Output

If the user selected **Round 1** or **Full Prep**, generate and save these 3 files to the current working directory.

---

### File 1: `interview-strategy.md`

Analyze the resume and job description to produce:

**Role Analysis**
- What the company actually needs — decode the real signals behind the JD language
- Top 3 priorities the hiring manager cares about most

**Your Positioning**
- How the user's background maps to each of the top 3 priorities
- The strongest 2-3 differentiators from their resume for this specific role

**Gap Analysis**
- Any skill or experience gaps between the resume and the JD requirements
- Concrete suggestions for how to address or reframe each gap in the interview

**Resume Tailoring Tips**
- 3-5 specific edits to the resume to improve alignment with this JD
- Keywords to add or emphasize

**Cover Letter Angle**
- The single story or thread that should anchor the cover letter for this role

**Likely Hiring Manager Questions**
- 10-15 questions the HM will probably ask based on the JD and the user's background
- For each: a coached answer framework referencing specific resume content

**Pre-Interview Research Checklist**
- Company product, recent news, competitors, team, and strategic direction
- 5-7 targeted research questions to answer before the interview

---

### File 2: `first-call-stories.md`

Generate 5 compelling STAR-format stories pulled directly from the resume. For each story:

- **Story Title** — a short, memorable label
- **Competency Mapped** — which specific JD requirement this story addresses
- **Situation** — the context and stakes
- **Task** — the user's specific responsibility
- **Action** — the decisions and steps taken (most important section — be specific)
- **Result** — quantifiable outcomes and business impact
- **Bridge** — 1-2 sentences connecting this story to what THIS company needs
- **Follow-up Talking Points** — 2-3 likely follow-up questions and brief answer guides

Each story should take 2-3 minutes when spoken aloud. Include a word-count estimate.

> Stories must be grounded in real resume content. Do not fabricate metrics.

---

### File 3: `project-discussion-points.md`

Generate structured discussion frameworks for 5 major projects from the resume. For each project:

- **Project Name & Company**
- **Project Overview & Context** — 2-3 sentences on what this was and why it mattered
- **Your Role & Responsibilities** — what you specifically owned
- **Key Challenges & How You Overcame Them** — the hardest 1-2 problems faced
- **Technologies, Tools & Methodologies Used**
- **Quantifiable Results** — metrics, KPIs, business outcomes
- **Lessons Learned** — what you would do differently
- **PM Competency Demonstrated** — explicitly map to JD requirements
- **Interview Talking Points** — 3-4 bullet points to hit when discussing this project

---

## Phase 3 — Round 2 Output

If the user selected **Round 2** or **Full Prep**, generate and save this file:

---

### File: `round2-prep.md`

#### Section 1 — Deep-Dive Behavioral Questions

Generate 10 hard behavioral and product questions based on the senior-level requirements in the JD. For each question:
- The question (written exactly as an interviewer would ask it)
- **Why they ask this** — what signal the interviewer is looking for
- **Coached answer framework** — how to structure the answer using the user's actual resume experience
- **Trap to avoid** — the most common wrong answer for this question

#### Section 2 — Case Study Scenarios

Build 2 mini product case studies tailored to the company's product area and the challenges implied by the JD:

For each scenario:
- **Problem statement** (grounded in what the company actually works on)
- **How to structure the answer** — a step-by-step framework
- **Key metrics to discuss** — what success looks like for this type of problem
- **Trade-offs to address** — the tensions the interviewer wants to see you navigate
- **Likely follow-up probes** — 2-3 follow-up questions to anticipate

#### Section 3 — Technical / Product Strategy Scenario

For AI PM or technical PM roles, generate one product or system design scenario relevant to the company's product space:

- **Scenario prompt** — written as the interviewer would present it
- **Structured walkthrough:**
  1. Clarify requirements and constraints
  2. Define success metrics
  3. High-level design or product approach
  4. Key trade-offs and decisions
  5. Risks and mitigations
- **What strong answers include** — 3-4 signals that show senior-level thinking

For non-technical PM roles, replace with a **prioritization or strategy scenario** instead.

#### Section 4 — Strategic Questions to Ask Interviewers

Generate 5 sharp, specific questions the user should ask — each covering a different dimension:

1. **Product Direction** — A question about technical or product strategy that shows you've done homework
2. **Team & Ways of Working** — A question about how the team operates, makes decisions, or handles disagreement
3. **Success in the Role** — "What does great look like in the first 90 days?"
4. **Biggest Product Challenge** — A question that invites the interviewer to talk about their hardest unsolved problem
5. **What Separates Top Performers** — A question about what distinguishes the best PMs on the team

For each question: include a note on **why this question is powerful** and what a strong answer from the interviewer looks like.

---

## Rules

- Do NOT generate generic responses — every output must reference specific details from the resume and JD
- Do NOT skip the intake phase — gathering resume + JD is mandatory before any generation
- Think like: senior PM hiring manager + executive recruiter + career coach, all in one
- For **AI PM roles**, go deeper on: agent architectures, evaluation frameworks, RAG/knowledge graphs, LLM product metrics, safety and guardrails, 0→1 model-integrated products
- All output files go to the **current working directory**
- Writing style: direct, specific, no hedging — strip all filler language
- Stories and project points must reference real metrics or resume content; do not fabricate numbers
- If the resume or JD is vague, ask one targeted clarifying question before generating, rather than guessing

---

## Output Checklist

Before completing, verify:

- [ ] `interview-strategy.md` created (Round 1 / Full Prep)
- [ ] `first-call-stories.md` created with 5 STAR stories (Round 1 / Full Prep)
- [ ] `project-discussion-points.md` created with 5 projects (Round 1 / Full Prep)
- [ ] `round2-prep.md` created with all 4 sections (Round 2 / Full Prep)
- [ ] Every section references specific resume content — no generic statements
- [ ] Every section references specific JD requirements — mapped explicitly
- [ ] No fabricated metrics, names, or company details
- [ ] Files saved to current working directory with correct filenames
