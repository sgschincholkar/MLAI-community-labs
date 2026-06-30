---
name: launch-checklist
description: Generate a complete product launch checklist for a feature or product release. Use when a PM is preparing to ship and needs to ensure nothing falls through the cracks across engineering, design, data, marketing, legal, support, and ops.
tools: AskUserQuestion, Write
---

## Goal

Produce a comprehensive, customized launch checklist that accounts for every team and function involved in shipping a product feature — from code freeze to post-launch monitoring.

---

## Behavior

Trigger when the user says:
- "create a launch checklist"
- "help me prepare to ship"
- "what do I need to do before launch"
- "launch plan for..."
- "go-live checklist"

---

## Phase 1 — Intake

Use `AskUserQuestion` to collect:

**Question 1 — What Are You Launching?**
Ask: "Describe the feature or product you're launching. What does it do, who is it for, and what platform is it on?"

**Question 2 — Launch Type**
Ask: "What type of launch is this? (1) Soft launch / internal beta, (2) Gradual rollout (percentage-based), (3) Full public launch, (4) Major version release"

**Question 3 — Launch Date**
Ask: "What is your target launch date? And is this a hard deadline or is there flexibility?"

**Question 4 — Teams Involved**
Ask: "Which teams are involved in this launch? Check all that apply: Engineering, Design, Data/Analytics, Marketing, Legal/Compliance, Customer Support, Sales, DevOps/Infrastructure, Executive"

**Question 5 — Risk Level**
Ask: "What is the risk level of this launch? (1) Low — small feature, limited blast radius, easy rollback (2) Medium — user-facing change, moderate exposure (3) High — payment flow, auth, data migration, major UX change, regulatory touch)"

**CRITICAL:** Do not generate the checklist until all 5 questions are answered.

---

## Phase 2 — Generate Launch Checklist

Write and save `launch-checklist-[feature]-[date].md` to the current working directory.

---

### Launch Overview

| Field | Value |
|-------|-------|
| Feature / Product | |
| Launch Type | |
| Target Launch Date | |
| Launch Owner (PM) | |
| Launch Risk Level | Low / Medium / High |
| Rollback Plan | [one sentence — how do we undo this if needed?] |

---

### Pre-Launch Checklist

Use ✅ / ⬜ / 🔴 (done / pending / blocked) to track each item.

---

#### Engineering & Technical Readiness

- ⬜ Code complete and merged to main branch
- ⬜ All P0/P1 bugs resolved; known P2s documented and accepted
- ⬜ Code review completed by at least 2 engineers
- ⬜ Feature flag configured — launch can be toggled without a deploy
- ⬜ Rollback procedure documented and tested
- ⬜ Performance benchmarks run — no regression from baseline
- ⬜ Load testing completed for expected peak traffic
- ⬜ API rate limits and timeout handling verified
- ⬜ Error handling tested — graceful degradation confirmed
- ⬜ Database migration tested on staging with production-size dataset
- ⬜ Security review completed (especially if auth, payments, PII involved)
- ⬜ Dependency audit — all third-party services confirmed available

---

#### Quality Assurance

- ⬜ QA regression suite passed on staging environment
- ⬜ PM acceptance testing completed on staging
- ⬜ Cross-browser / cross-device testing completed
- ⬜ Accessibility audit (WCAG 2.1 AA minimum)
- ⬜ Edge cases documented and tested
- ⬜ User acceptance testing (UAT) with pilot users completed (if applicable)
- ⬜ Sign-off from QA lead

---

#### Data & Analytics

- ⬜ All tracking events instrumented and verified firing correctly
- ⬜ Dashboard or monitoring view created for launch metrics
- ⬜ Baseline metrics captured (pre-launch snapshot)
- ⬜ Alert thresholds configured for key metrics
- ⬜ Data pipeline confirmed for new event types
- ⬜ Analytics team briefed on what to watch post-launch

---

#### Design & Content

- ⬜ Final design reviewed and approved by design lead
- ⬜ All copy reviewed (UI strings, error messages, emails, notifications)
- ⬜ Empty states designed and implemented
- ⬜ Loading and error states designed and implemented
- ⬜ Onboarding / tooltip copy written and reviewed
- ⬜ Help documentation written and published

---

#### Legal & Compliance

- ⬜ Legal review completed (if new data collection, new markets, payments)
- ⬜ Privacy policy updated (if applicable)
- ⬜ Terms of service updated (if applicable)
- ⬜ GDPR / CCPA compliance verified (if applicable)
- ⬜ Security penetration test completed (for high-risk launches)

---

#### Customer Support

- ⬜ Support team briefed on new feature functionality
- ⬜ FAQ / knowledge base article published
- ⬜ Support ticket templates updated for new feature
- ⬜ Known issues list shared with support team
- ⬜ Escalation path documented for launch-day issues

---

#### Marketing & Communications (Full Launch Only)

- ⬜ Launch announcement written and approved
- ⬜ Blog post / changelog entry ready to publish
- ⬜ Social media posts scheduled (if applicable)
- ⬜ Email announcement drafted and reviewed (if applicable)
- ⬜ Internal announcement to company ready (Slack, all-hands)
- ⬜ Press/media outreach planned (if applicable)
- ⬜ Sales enablement materials updated

---

#### Infrastructure & Operations

- ⬜ Monitoring alerts configured (error rate, latency, availability)
- ⬜ On-call rotation confirmed for launch window
- ⬜ Runbook created for top 3 likely incidents
- ⬜ CDN / caching configuration reviewed
- ⬜ Backup and recovery procedures verified

---

### Launch Day Checklist

- ⬜ War room / launch channel set up (Slack #launch-[feature-name])
- ⬜ All stakeholders notified: launch is starting
- ⬜ Feature flag enabled for target % of traffic
- ⬜ Monitoring dashboard open and being watched
- ⬜ First 30-minute metrics check — all green?
- ⬜ First 2-hour metrics check — primary metric trending correctly?
- ⬜ Support team: any unusual ticket spike?
- ⬜ Error rate: within acceptable threshold?
- ⬜ Full rollout confirmed (or rollback decision made)

---

### Post-Launch Checklist (24–72 hours)

- ⬜ 24-hour metrics review completed
- ⬜ 72-hour metrics review completed
- ⬜ Any P0/P1 issues found — resolved or triaged
- ⬜ User feedback collected and reviewed
- ⬜ Launch retrospective scheduled
- ⬜ A/B test results reviewed (if applicable)
- ⬜ Stakeholder update sent with launch results

---

### Rollback Criteria

Define in advance when you would roll back:

| Condition | Threshold | Action |
|-----------|----------|--------|
| Error rate | >X% above baseline | Immediate rollback |
| Latency P99 | >Xms above baseline | Investigate → rollback if not resolved in 30min |
| Primary metric | >X% degradation | Investigate → rollback if confirmed |
| Support ticket spike | >X tickets/hour | Escalate → rollback if systemic issue |

---

## Rules

- Every launch regardless of size needs a rollback plan
- Do not mark Engineering items complete without QA sign-off
- Launch day monitoring must be a named person, not "the team"
- Post-launch review is not optional — close the loop on every launch
