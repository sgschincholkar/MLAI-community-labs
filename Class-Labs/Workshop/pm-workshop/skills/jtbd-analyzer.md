---
name: jtbd-analyzer
description: Run a Jobs-to-be-Done analysis for a product or feature. Use when a PM wants to understand the underlying user motivation behind a feature request, reframe requirements around user jobs, evaluate whether a feature solves the right problem, or build a deeper user understanding for a PRD.
tools: AskUserQuestion, Write, WebSearch
---

## Goal

Uncover the real "job" users are hiring a product to do — not what they ask for, but what outcome they are truly trying to achieve. Produce a JTBD analysis that reframes product decisions around user progress, not feature lists.

---

## Behavior

Trigger when the user says:
- "run a JTBD analysis"
- "what job is this feature doing"
- "understand why users really want this"
- "jobs to be done for..."
- "reframe this around user outcomes"

---

## Phase 1 — Intake

Use `AskUserQuestion` to collect:

**Question 1 — Product / Feature**
Ask: "What product, feature, or user request are we analyzing? Describe what the user is asking for."

**Question 2 — User Context**
Ask: "Who is the user? Describe their role, their typical workday, and what they are responsible for achieving."

**Question 3 — Trigger Situation**
Ask: "In what specific situation does a user turn to this product or request this feature? Describe the moment — what just happened that prompts them to act?"

**Question 4 — Current Behavior**
Ask: "How does the user solve this problem today, before your product or feature exists? What is their workaround — even a bad one?"

**Question 5 — Success Picture**
Ask: "What does 'done' look like for the user? If this feature works perfectly, what has changed in their work or life?"

**CRITICAL:** Do not generate the analysis until all 5 questions are answered.

---

## Phase 2 — Research (Optional)

If a product domain is specified, use `WebSearch` to find:
- User reviews or forums discussing the pain (Reddit, G2, Hacker News)
- Any published JTBD research in the domain
- Competitor positioning language that reveals what job they claim to solve

---

## Phase 3 — JTBD Analysis

Write and save `jtbd-analysis-[product]-[date].md` to the current working directory.

---

### The Core Job Statement

Write the job statement in the canonical JTBD format:

> **When** [situation that triggers the need],
> **I want to** [the underlying motivation / desired progress],
> **So I can** [the outcome that matters to them].

Write 1 primary job statement and 2-3 related job statements at different levels of abstraction (the "job ladder").

**Job Ladder:**
```
High-level job:  "Reduce business risk from vendor relationships"
     ↑
Mid-level job:   "Catch unfavorable contract terms before signing"
     ↑
Functional job:  "Review a new contract quickly and flag key clauses"
     ↑
Feature request: "Highlight payment terms and liability caps in uploaded contracts"
```

The feature request is at the bottom. PMs should design for the mid-level job.

---

### Forces Analysis

What forces push the user toward and away from a new solution?

#### Forces Pushing Toward Change (Why They'd Hire Your Product)
| Force | Strength | Example |
|-------|----------|---------|
| **Push** — pain with current situation | H/M/L | "Reviewing contracts manually takes 3 hours" |
| **Pull** — attraction to the new solution | H/M/L | "AI review takes 5 minutes" |

#### Forces Pulling Away From Change (Why They'd Stick With Status Quo)
| Force | Strength | Example |
|-------|----------|---------|
| **Anxiety** — fear of the new solution | H/M/L | "What if AI misses something?" |
| **Habit** — inertia from current behavior | H/M/L | "I've always used my lawyer for this" |

**Insight:** A product adoption problem is often not about features — it's about reducing anxieties and habits. List 2-3 specific product decisions that would reduce the two biggest resistance forces.

---

### Jobs Hierarchy

Decompose the core job into its component jobs:

| Job Type | Job Statement | Currently Solved? | How? |
|----------|--------------|-------------------|------|
| **Functional job** | The practical task | Yes/No/Poorly | |
| **Emotional job** | How they want to feel | Yes/No/Poorly | |
| **Social job** | How they want to be perceived | Yes/No/Poorly | |

**Example:**
- Functional: "Identify all high-risk clauses in a contract"
- Emotional: "Feel confident the contract is safe to sign"
- Social: "Be seen as a thorough, credible professional by my team"

---

### Desired Outcomes (Outcome-Driven Innovation)

List the specific outcomes the user wants when executing the job. For each outcome:

**Format:** [Direction] + [Metric] + [Object] + [Context]
*Example: "Minimize the time it takes to identify all high-risk clauses in a 50-page contract"*

| Outcome Statement | Importance (1–5) | Satisfaction Today (1–5) | Opportunity Score* |
|------------------|------------------|--------------------------|-------------------|
| ... | | | |

*Opportunity Score = Importance + (Importance − Satisfaction)*
*High score (>10) = underserved outcome = product opportunity*

---

### The Job Haiku (Synthesis)

Distill the entire analysis into a single, memorable statement:

> **[User type]** needs a way to **[core job]**
> so they can feel **[emotional outcome]**
> without **[biggest anxiety or sacrifice]**.

*Example: "A startup founder needs a way to catch risky contract terms in minutes so they can feel confident about vendor deals without depending on expensive legal review."*

---

### Implications for Product Decisions

| JTBD Insight | Current Feature/Approach | Recommended Change |
|-------------|--------------------------|-------------------|
| The real job is X, not Y | We built Z | Refocus on... |
| Biggest anxiety is X | We don't address it | Add... |
| Social job is X | Invisible in product | Surface via... |

---

### What This Changes About the PRD

Based on the JTBD analysis, list 3-5 specific changes to make to the product spec:

1. **Requirement to add:** [what and why — which job it serves]
2. **Requirement to reframe:** [how to rewrite it around the job, not the feature]
3. **Requirement to remove:** [what solves the wrong job]
4. **Success metric to change:** [old metric → new metric that tracks job completion]
5. **Positioning language to use:** [how to describe the product in terms of the job]

---

## Rules

- Never confuse what users ask for with what job they need done — these are different things
- The job ladder is mandatory — the analysis must show all levels of abstraction
- Emotional and social jobs are as real as functional jobs — do not skip them
- Desired outcomes must be measurable — reject vague outcomes like "feel confident"
- The final "Implications" section is why this analysis exists — it must tie back to specific product decisions
