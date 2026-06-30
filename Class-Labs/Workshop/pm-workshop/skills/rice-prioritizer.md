---
name: rice-prioritizer
description: Run RICE scoring to prioritize a feature backlog. Use when a PM needs to rank features, decide what to build next, defend prioritization decisions to stakeholders, or create a data-backed roadmap. Collects the feature list and scoring criteria via AskUserQuestion.
tools: AskUserQuestion, Write, WebSearch
---

## Goal

Help a PM score and rank a list of features or initiatives using the RICE framework (Reach × Impact × Confidence ÷ Effort). Produce a prioritized backlog with rationale that can be shared with engineering and leadership.

---

## Behavior

Trigger when the user says:
- "prioritize my backlog"
- "RICE score these features"
- "what should we build first"
- "help me rank these initiatives"
- "create a prioritized roadmap"

---

## Phase 1 — Intake

Use `AskUserQuestion` to collect:

**Question 1 — Feature List**
Ask: "List the features or initiatives you want to prioritize. Paste them as a numbered or bulleted list. Include a one-sentence description for each — if you can."

**Question 2 — Time Horizon**
Ask: "What time period are we prioritizing for? (e.g., next sprint, next quarter, next 6 months, annual roadmap)"

**Question 3 — User Base Size**
Ask: "How large is your total addressable user base for these features? Give me a rough number so I can calibrate Reach scores. (e.g., 10K active users, 500K MAU, 2M registered accounts)"

**Question 4 — Scoring Context**
Ask: "Any constraints I should factor in? For example: features that are already committed, regulatory requirements, dependencies between features, or features that are off the table."

**Question 5 — Business Goal**
Ask: "What is the single most important business goal for this period? (e.g., reduce churn, grow revenue, improve activation, hit a compliance deadline)"

**CRITICAL:** Do not score until all 5 questions are answered.

---

## Phase 2 — RICE Scoring

Score each feature across 4 dimensions. Apply these calibrated scales:

### Reach (users/time period)
How many users will this feature affect in the time period?
- Use the user base size provided as the ceiling
- Express as absolute number: e.g., 5,000 users/quarter

### Impact (multiplier: 0.25 / 0.5 / 1 / 2 / 3)
How much does this move the needle for each user it reaches?
| Score | Meaning |
|-------|---------|
| 3 | Massive — fundamentally changes how they use the product |
| 2 | High — significantly improves a core workflow |
| 1 | Medium — noticeable improvement |
| 0.5 | Low — minor quality-of-life improvement |
| 0.25 | Minimal — most users won't notice |

### Confidence (%)
How confident are you in the Reach and Impact estimates?
| % | Meaning |
|---|---------|
| 100% | Data-backed — you have evidence from user research or analytics |
| 80% | Strong — informed opinion with some supporting data |
| 50% | Medium — educated guess |
| 20% | Low — speculation |

### Effort (person-months)
Total work across all teams (engineering, design, PM, QA):
- 0.5 = 1-2 weeks
- 1 = ~1 month
- 2 = ~2 months
- 3 = ~1 quarter
- 6+ = multi-quarter

### RICE Formula
`RICE Score = (Reach × Impact × Confidence) ÷ Effort`

---

## Phase 3 — Generate Prioritization Report

Write and save `rice-prioritization-[date].md` to the current working directory.

---

### Prioritized Backlog

| Rank | Feature | Reach | Impact | Confidence | Effort | RICE Score |
|------|---------|-------|--------|------------|--------|------------|
| 1 | ... | ... | ... | ... | ... | ... |
| 2 | ... | ... | ... | ... | ... | ... |
| ... | | | | | | |

---

### Scoring Rationale

For each feature, provide:
- **Reach rationale:** Why this number (who specifically will use it?)
- **Impact rationale:** Why this multiplier (what workflow does it change?)
- **Confidence rationale:** What data or assumption drives this?
- **Effort rationale:** What is the biggest work driver?

---

### Strategic Lens

Beyond pure RICE score, flag any features that warrant a re-rank due to:

| Feature | Adjustment | Reason |
|---------|------------|--------|
| ... | Bump up | Strategic must-do (committed, regulatory, CEO ask) |
| ... | Bump down | Dependency blocked, team capacity constraint |
| ... | Hold | Needs more research before scoring is credible |

---

### Recommended Roadmap Cut

Given the time horizon and team capacity:

**Build Now (Top Priority):**
- Feature 1 — [why]
- Feature 2 — [why]

**Build Next (Queued):**
- Feature 3 — [dependency or timing reason]
- Feature 4

**Defer or Revisit:**
- Feature X — [what needs to change before this rises in priority]

---

### Assumptions & Risks

| Assumption | If Wrong, Then... | How to Validate |
|-----------|-------------------|----------------|
| ... | ... | ... |

---

## Rules

- Show your math for every score — no black-box rankings
- Flag features where confidence is <50% and recommend how to increase it (user research, A/B test, prototype)
- If two features are within 10% of each other in RICE score, call them a tie and let the business goal break the tie
- Never let RICE override a hard constraint (regulatory deadlines, committed features) — flag those separately
- Output must be shareable with engineering and leadership as-is
