---
name: stakeholder-update
description: Generate a professional stakeholder update for a product initiative — weekly status, milestone summary, or executive briefing. Use when a PM needs to communicate progress, escalate a blocker, or present a product update to leadership, investors, or cross-functional partners.
tools: AskUserQuestion, Write
---

## Goal

Produce a crisp, well-structured stakeholder communication that conveys the right level of detail for the audience — whether it is a weekly status email, a leadership deck narrative, or a cross-functional milestone update.

---

## Behavior

Trigger when the user says:
- "write a stakeholder update"
- "send a project status"
- "draft my leadership update"
- "executive summary of where we are"
- "weekly PM update"
- "communicate this to my skip level"

---

## Phase 1 — Intake

Use `AskUserQuestion` to collect:

**Question 1 — Audience**
Ask: "Who is receiving this update? (e.g., your direct manager, VP/Director, C-suite, cross-functional partners, external investors). This determines length and detail level."

**Question 2 — Format**
Ask: "What format do you need? (1) Email, (2) Slack/Teams message, (3) Written narrative for a doc/deck, (4) Executive one-pager"

**Question 3 — Project Status**
Ask: "What is the current state of the project? Tell me: what was the goal, what have you shipped or completed, what is in progress, what is blocked, and what is next."

**Question 4 — Key Metrics**
Ask: "What are the key metrics for this project and where do they stand today? Give me the numbers — even rough ones."

**Question 5 — Headline**
Ask: "If you had to summarize this update in one sentence — the single most important thing stakeholders need to know — what is it?"

**Question 6 — Asks or Decisions Needed**
Ask: "Is there anything you need from this audience? A decision, unblocking, budget, headcount, a review? Be specific."

**CRITICAL:** Do not write the update until all 6 questions are answered.

---

## Phase 2 — Generate Update

Write and save `stakeholder-update-[project]-[date].md` to the current working directory.

Generate the appropriate format based on the audience answer:

---

### Format A — Executive Email

**Subject:** [Project Name] — [One-line status: On Track / At Risk / Blocked / Milestone Hit]

**TL;DR:**
One sentence. What is the most important thing they need to know.

**Status:** 🟢 On Track / 🟡 At Risk / 🔴 Blocked

**What We Shipped This Period:**
- [Specific deliverable] — [impact or metric]
- [Specific deliverable] — [impact or metric]

**Key Metrics:**
| Metric | Last Period | This Period | Target |
|--------|-------------|-------------|--------|
| ... | | | |

**In Progress:**
- [Item] — [expected completion]

**Blockers / Decisions Needed:**
- 🔴 [Blocker] — **Need:** [specific ask] by [date]

**What's Next (Next 2 Weeks):**
- [Milestone or deliverable] — [date]

---

### Format B — Slack / Teams Message

```
*[Project Name] Update — [Date]*

*Status:* 🟢 On Track

*This week:*
• [Shipped item 1]
• [Shipped item 2]

*Metrics:*
• [Metric]: [value] (target: [value])

*Next week:*
• [Plan item 1]
• [Plan item 2]

*Needs from you:*
• [Decision / unblock / review needed]
```

---

### Format C — Written Narrative (Doc / Deck)

**Headline:** [The single most important statement about project state]

**Background (2 sentences):**
What this initiative is and why it matters.

**Progress This Period:**
Describe in narrative form what shipped, what was learned, and what changed. Reference metrics concretely.

**Current Status by Workstream:**

| Workstream | Owner | Status | Notes |
|-----------|-------|--------|-------|
| ... | ... | 🟢/🟡/🔴 | ... |

**Risks & Mitigations:**

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| ... | H/M/L | H/M/L | ... |

**Decisions Requested:**
1. [Decision needed] — [context for the decision] — [recommended path]

**Upcoming Milestones:**

| Milestone | Date | Owner | Dependencies |
|-----------|------|-------|-------------|
| ... | | | |

---

### Format D — Executive One-Pager

**[PROJECT NAME] — EXECUTIVE BRIEF**
**Date:** | **Owner:** | **Status:**

---

**What We're Building & Why**
[2 sentences max]

**Where We Are**
[2-3 bullets of concrete progress]

**The Number That Matters**
[Single most important metric and what it means]

**What We Need**
[Single ask in one sentence]

**Next Decision Point**
[Date and what will be decided]

---

## Rules

- Lead with the headline — never bury the most important thing
- Status must be honest: 🔴 when it is 🔴, not 🟡 to avoid discomfort
- Metrics are mandatory — "good progress" without numbers is meaningless
- Asks must be specific: who needs to decide what by when
- Match the reading level to the audience — C-suite gets bullets, manager gets detail
- Remove all jargon the audience does not use
