---
name: sprint-planner
description: Plan a complete sprint from a backlog of user stories. Use when a PM or Scrum Master needs to select stories for an upcoming sprint, balance team capacity against story points, set a clear sprint goal, and produce a sprint plan document ready for the kickoff meeting.
tools: AskUserQuestion, Write
---

## Goal

Convert a backlog of user stories into a structured, capacity-balanced sprint plan — with a clear goal, story assignments, and a realistic commitment the team can stand behind.

---

## Behavior

Trigger when the user says:
- "plan my next sprint"
- "sprint planning help"
- "pick stories for the sprint"
- "create a sprint plan"
- "how much can we fit in this sprint"

---

## Phase 1 — Intake

Use `AskUserQuestion` to collect:

**Question 1 — Team Capacity**
Ask: "How many engineers are on the team and what is their capacity for this sprint? (e.g., 4 engineers × 8 points each = 32 points, or 3 full-time + 1 at 50%). Include any PTO, holidays, or on-call rotations that reduce capacity."

**Question 2 — Sprint Goal**
Ask: "What is the single most important outcome of this sprint? This becomes the sprint goal — the team should be able to explain it in one sentence. What would make this sprint a success even if not everything is completed?"

**Question 3 — Backlog**
Ask: "Share your prioritized backlog. Paste the user stories with their story point estimates. If you have them in a tool (Jira, Linear, Notion), describe the top 10-15 stories. Include ID, title, and points for each."

**Question 4 — Carryover**
Ask: "Are there any stories carrying over from the previous sprint? What is their status — partially done, blocked, or just not started?"

**Question 5 — Constraints**
Ask: "Any sprint-level constraints? For example: a dependency on another team, a deadline mid-sprint, a demo scheduled, or a tech debt ceiling you maintain."

**CRITICAL:** Do not generate the sprint plan until all 5 questions are answered.

---

## Phase 2 — Capacity Calculation

Calculate the sprint's available capacity:

```
Total team points = (engineers × avg velocity per engineer)
Buffer (20% for unexpected) = total × 0.2
Net committable points = total - buffer - carryover points
```

Recommend a commitment that is 80% of net capacity — avoid over-committing.

---

## Phase 3 — Generate Sprint Plan

Write and save `sprint-plan-[sprint-number]-[date].md` to the current working directory.

---

### Sprint Overview

| Field | Value |
|-------|-------|
| Sprint Number / Name | |
| Start Date | |
| End Date | |
| Sprint Goal | |
| Team Capacity | X points total |
| Carryover Points | X points |
| Planned Commitment | X points |
| Buffer Held | X points |

---

### Sprint Goal

> **In this sprint, we will [accomplish X] so that [user/business outcome].**
> **We'll know we succeeded when [measurable condition].**

---

### Committed Stories

Stories the team is committing to complete this sprint:

| ID | Title | Points | Assignee (if known) | Dependency |
|----|-------|--------|---------------------|------------|
| US-001 | | | | |
| US-002 | | | | |
| ... | | | | |
| **Total** | | **X pts** | | |

---

### Carryover Stories

Stories from previous sprint, continued in this sprint:

| ID | Title | Points Remaining | Status | Blocker (if any) |
|----|-------|-----------------|--------|-----------------|
| ... | | | In Progress / Blocked | |

---

### Stretch Goals (If Capacity Allows)

Stories to pull in only if committed work completes early:

| ID | Title | Points | Why Stretch (not committed) |
|----|-------|--------|-----------------------------|
| ... | | | |

---

### Capacity Breakdown

| Engineer | Capacity (days) | Estimated Points | Assigned Stories |
|----------|-----------------|-----------------|-----------------|
| [Name or Eng 1] | | | US-001, US-003 |
| ... | | | |
| **Team Total** | | **X pts** | |

**Capacity risks:**
- [Name] is on-call week 2 — reduce capacity by 20%
- Sprint includes [holiday] — [X] working days, not 10
- [Name] has a dependency on Platform team response before US-005 can start

---

### Dependencies & Blockers

| Story | Depends On | Owner | Expected By |
|-------|-----------|-------|------------|
| US-005 | Platform API endpoint | Platform team | Day 3 |
| US-008 | Design final mockup | Design lead | Day 1 |

---

### Definition of Done (Sprint Level)

For this sprint, a story is "done" when:
- [ ] Code reviewed and merged
- [ ] Unit tests written and passing
- [ ] Deployed to staging
- [ ] PM acceptance confirmed
- [ ] No P0/P1 bugs introduced

---

### Sprint Risks

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| Platform dependency delayed | Medium | High | Start US-005 frontend in parallel; wire API last |
| Design not finalized on Day 1 | Low | Medium | PM to confirm with design today |
| Sprint commitment is too aggressive | Low | Medium | Stretch goals defined — can de-scope safely |

---

### Sprint Kickoff Agenda

Use this as the structure for the sprint planning meeting:

1. **Sprint Goal** (5 min) — PM presents and team aligns
2. **Capacity Check** (5 min) — confirm who is available, note PTO/on-call
3. **Backlog Walk** (20 min) — PM walks committed stories, engineers ask clarifying questions
4. **Story Assignment** (10 min) — engineers self-select or PM assigns stories
5. **Dependency Review** (5 min) — flag any external blockers to resolve on Day 1
6. **Commitment** (5 min) — team verbally commits to the sprint goal

---

## Rules

- Never commit 100% of team capacity — 80% is the target to account for meetings, reviews, and unexpected issues
- One sprint goal only — multiple goals mean no goal
- Carryover stories reduce new capacity, not new commitment
- Stretch goals must be genuinely optional — if the team will feel bad not finishing them, they are commitments
- The sprint plan is a forecast, not a contract — communicate this to stakeholders
