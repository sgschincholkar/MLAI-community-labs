---
name: user-story-gen
description: Generate a complete set of user stories and acceptance criteria from a PRD or feature description. Use when a PM needs to break down requirements into sprint-ready stories, create a story map, or prepare a backlog for engineering grooming.
tools: AskUserQuestion, Write, Read
---

## Goal

Transform a PRD or feature description into a complete, sprint-ready set of user stories with acceptance criteria, edge cases, and story points estimation — formatted for direct import into Jira, Linear, or any backlog tool.

---

## Behavior

Trigger when the user says:
- "generate user stories"
- "break this PRD into stories"
- "write acceptance criteria"
- "create a story map"
- "prepare backlog for engineering"

---

## Phase 1 — Intake

Use `AskUserQuestion` to collect:

**Question 1 — Source Document**
Ask: "Share the PRD or feature description to generate stories from. Paste text or reference a file with @filename."

**Question 2 — Personas**
Ask: "Who are the user types / personas involved? List them (e.g., Admin, End User, Guest, API Consumer). This determines how many story angles we need."

**Question 3 — Sprint Goal**
Ask: "What is the sprint or milestone goal? This helps me separate MVP stories from stretch goals."

**Question 4 — Engineering Context**
Ask: "Any technical context I should know? (e.g., this is a new microservice, it builds on existing auth system, we use REST not GraphQL, frontend is React). This affects how I word the technical criteria."

**Question 5 — Story Format**
Ask: "Which backlog format do you use? (1) Classic: As a [user], I want [action] so that [outcome] — (2) Job story: When [situation], I want to [motivation], so I can [outcome] — (3) Simple task format"

**CRITICAL:** Do not generate until all 5 questions are answered.

---

## Phase 2 — Story Mapping

Before writing individual stories, create a story map structure:

**Epic → Feature → Story hierarchy:**

```
Epic (the big user goal)
  └── Feature (a distinct capability)
       └── Story (a single deliverable increment)
            └── Task (implementation detail — for engineering, not PM)
```

Identify all epics first, then break each into features, then stories.

---

## Phase 3 — Generate Stories

Write and save `user-stories-[feature-name].md` to the current working directory.

---

### Story Map Overview

| Epic | Feature | Story Count | Priority |
|------|---------|-------------|----------|
| ... | ... | ... | MVP / V2 |

---

### User Stories

For each story, use this full template:

---

**Story ID:** US-[number]
**Epic:** [parent epic]
**Feature:** [parent feature]
**Priority:** Must Have / Should Have / Nice to Have
**Story Points:** [1 / 2 / 3 / 5 / 8 / 13] — with brief rationale

**Story:**
> As a [persona], I want to [action] so that [outcome/benefit].

**Context:**
One sentence on why this story matters in the larger user flow.

**Acceptance Criteria:**
Written in Gherkin format (Given / When / Then):

```
Given [precondition or starting state]
When [user action or system event]
Then [expected outcome]
And [additional assertion if needed]
```

Provide 3-5 acceptance criteria per story covering:
- Happy path
- Validation/error handling
- Edge cases
- Performance expectations (if relevant)
- Accessibility (if relevant)

**Out of Scope for This Story:**
- List 2-3 things this story explicitly does NOT cover (prevents scope creep)

**Dependencies:**
- Other stories that must be done first (reference by ID)
- External systems or APIs this touches

**Definition of Done:**
- [ ] Code reviewed and merged
- [ ] Unit tests written and passing
- [ ] Acceptance criteria verified by PM
- [ ] Deployed to staging
- [ ] [Feature-specific items added here]

---

### Edge Cases & Error Stories

Generate dedicated stories for:
- Empty states (first time user, no data)
- Error states (network failure, invalid input, permission denied)
- Concurrent access (two users editing the same record)
- Performance degradation (what happens under load)
- Accessibility (keyboard navigation, screen reader)

---

### Story Points Summary

| Priority Tier | Story Count | Total Points | Estimated Sprints (2-week, 5-dev team) |
|--------------|-------------|--------------|---------------------------------------|
| Must Have (MVP) | | | |
| Should Have | | | |
| Nice to Have | | | |
| **Total** | | | |

---

### Backlog Import Format

Generate a CSV-compatible summary for Jira/Linear import:

```
ID, Title, Epic, Priority, Points, Description
US-001, "User can upload contract file", "Contract Analysis", "Must Have", 3, "As an analyst..."
```

---

## Rules

- Every acceptance criterion must be testable — reject vague criteria like "works correctly"
- Use specific numbers in criteria where possible ("within 3 seconds", "file size max 10MB")
- Every story must be independent and deliverable in a single sprint
- If a story is too big (>8 points), break it into sub-stories
- Non-happy-path stories are not optional — error handling is a first-class citizen
