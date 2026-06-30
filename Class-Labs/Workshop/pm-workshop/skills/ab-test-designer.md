---
name: ab-test-designer
description: Design a rigorous A/B test plan for a product feature or UX change. Use when a PM wants to validate a hypothesis before a full build, test two versions of a feature, or create an experiment spec that data science can implement.
tools: AskUserQuestion, Write, WebSearch
---

## Goal

Produce a complete, statistically sound A/B test plan that a PM can hand directly to a data scientist or engineer to implement — with clear hypothesis, metrics, sample size, duration, and decision criteria.

---

## Behavior

Trigger when the user says:
- "design an A/B test"
- "help me test this hypothesis"
- "create an experiment plan"
- "how do we validate this feature"
- "run an experiment on..."

---

## Phase 1 — Intake

Use `AskUserQuestion` to collect:

**Question 1 — What Are You Testing?**
Ask: "Describe the change you want to test. What is the control (current experience) and what is the variant (proposed change)?"

**Question 2 — Hypothesis**
Ask: "What is your hypothesis? Complete this sentence: 'If we [change], then [metric] will [increase/decrease] because [reason].'"

**Question 3 — Primary Metric**
Ask: "What is the ONE metric that determines if this test succeeds? (e.g., conversion rate, click-through rate, 7-day retention, revenue per user)"

**Question 4 — User Base**
Ask: "How many eligible users enter this experience per day/week? Give me your best estimate."

**Question 5 — Minimum Detectable Effect**
Ask: "What is the smallest improvement worth shipping? (e.g., a 5% lift in conversion, 2% improvement in retention, $0.50 increase in ARPU). This determines how long the test runs."

**Question 6 — Constraints**
Ask: "Any constraints? (e.g., can only test on mobile, can't affect paying users, must complete before [date], specific segments to include/exclude)"

**CRITICAL:** Do not design the test until all 6 questions are answered.

---

## Phase 2 — Statistical Calculations

Calculate the following:

**Sample Size per Variant:**
Using standard parameters (95% confidence, 80% statistical power):
- Baseline conversion rate: [from intake or estimated]
- Minimum detectable effect: [from intake]
- Required sample size: [calculate or estimate]

**Test Duration:**
- Daily/weekly eligible users ÷ variants ÷ sample size needed = days to run

**Guardrail Metrics:**
Identify 3-5 metrics that must NOT degrade during the test (even if primary metric improves).

---

## Phase 3 — Generate Experiment Plan

Write and save `ab-test-[name]-[date].md` to the current working directory.

---

### Experiment Brief

| Field | Value |
|-------|-------|
| Experiment Name | |
| Owner (PM) | |
| Data Science Contact | |
| Status | Draft / Approved / Running / Concluded |
| Start Date | |
| End Date | |

---

### Hypothesis

**If we** [describe the change]
**Then** [primary metric] will [increase/decrease] by approximately [MDE]%
**Because** [the causal mechanism — why this change creates the outcome]
**We'll know we're wrong if** [what would disprove the hypothesis]

---

### Control vs. Variant

| | Control (A) | Variant (B) |
|--|-------------|-------------|
| Description | Current experience | Proposed change |
| Key Difference | — | [what specifically changes] |
| Expected User Experience | [describe] | [describe] |

*(Add Variant C, D if testing multiple versions)*

---

### Metrics

**Primary Metric** (determines win/loss):
- Metric name: [e.g., "7-day activation rate"]
- Definition: [exact formula — what counts as an activation]
- Baseline value: [current rate]
- Minimum Detectable Effect: [e.g., +5% relative, meaning 10% → 10.5%]

**Secondary Metrics** (directional signals, not decision criteria):
| Metric | Definition | Expected Direction | Why We're Watching |
|--------|-----------|--------------------|-------------------|
| ... | | ↑ / ↓ / ~ | |

**Guardrail Metrics** (must not degrade):
| Metric | Threshold | Action if Violated |
|--------|----------|-------------------|
| Revenue per user | -2% max | Stop test immediately |
| Error rate | +0.5% max | Escalate to eng |
| Support tickets | +10% max | Investigate |

---

### Statistical Parameters

| Parameter | Value | Rationale |
|-----------|-------|-----------|
| Confidence Level | 95% | Standard — reduce to 90% for low-risk tests |
| Statistical Power | 80% | Standard |
| Sample Size (per variant) | [calculated] | |
| Eligible Users per Day | [from intake] | |
| Traffic Split | 50/50 | Adjust if variant is riskier |
| Minimum Test Duration | [calculated] days | |
| Maximum Test Duration | [calculated + 20%] | Stops test from running indefinitely |

---

### Targeting & Segmentation

**Who is included:**
- Platform: [web / iOS / Android / all]
- User segment: [new users / returning / all / specific cohort]
- Geography: [global / specific regions]
- Other filters: [paying vs. free, activation status, etc.]

**Who is excluded:**
- [e.g., employees, beta users, users in other concurrent experiments]

**Randomization unit:** [user_id / session_id / device_id]
*(Use user_id for most experiments to prevent exposure pollution)*

---

### Instrumentation Requirements

Events that must be tracked for this experiment:

| Event Name | Trigger | Properties to Capture |
|------------|---------|----------------------|
| `experiment_exposed` | User enters experiment | variant, user_id, timestamp |
| `[primary metric event]` | [trigger] | [properties] |
| ... | | |

---

### Decision Criteria

**Ship Variant if:**
- Primary metric improvement ≥ MDE with p < 0.05
- No guardrail metric breaches
- Secondary metrics neutral or positive

**Do Not Ship if:**
- Primary metric flat or negative
- Any guardrail metric breach (regardless of primary result)
- Test did not reach statistical significance by max duration

**Investigate Further if:**
- Mixed results across segments (e.g., wins on mobile, loses on desktop)
- Secondary metrics conflict with primary metric

---

### Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| Novelty effect (users react to newness, not value) | Run test at minimum 2 business cycles |
| Segment contamination | Ensure randomization at user level |
| External events skewing results | Note any major launches, holidays, or news events during test window |
| Multiple comparison inflation | Correct for multiple primary metrics with Bonferroni if needed |

---

### Post-Test Analysis Plan

After the test concludes:
1. Check primary metric significance
2. Review all guardrail metrics
3. Segment analysis: by device, user age, user tier, geography
4. Long-term retention check (run holdout for 2-4 additional weeks)
5. Write experiment retrospective — what we learned regardless of result

---

## Rules

- One primary metric per experiment — testing multiple primary metrics inflates false positives
- Never stop a test early because it "looks good" — pre-commit to the duration
- A/A test recommendation: if this is the first experiment on a surface, run an A/A test first to validate infrastructure
- Document the hypothesis before seeing any results — prevents HARKing (Hypothesizing After Results are Known)
