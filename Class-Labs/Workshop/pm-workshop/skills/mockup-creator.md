---
name: mockup-creator
description: Generate functional HTML/CSS UI mockups directly from a PRD or feature description. Use when a PM wants to visualize a product before engineering starts, create something to show stakeholders, or generate a design starting point from product requirements.
tools: AskUserQuestion, Write, Read
---

## Goal

Turn a PRD or feature description into interactive HTML/CSS mockups that a PM can show to stakeholders, share with design, or hand to engineering as a UI reference. No design tool needed — Claude builds it directly.

---

## Behavior

Trigger when the user says:
- "create mockups"
- "build a wireframe from my PRD"
- "show me what this would look like"
- "generate a UI prototype"
- "make something I can show stakeholders"

---

## Phase 1 — Intake

Use `AskUserQuestion` to collect:

**Question 1 — PRD or Feature Description**
Ask: "Share your PRD or describe the feature I should mockup. You can paste text or reference a file with @filename."

**Question 2 — Screens Needed**
Ask: "Which specific screens do you need? For example: homepage, dashboard, upload flow, results page, settings. List the ones that matter most."

**Question 3 — User & Context**
Ask: "Who is the user and what are they trying to accomplish on each screen? Give me their goal in one sentence per screen."

**Question 4 — Style Direction**
Ask: "Any style preferences? (e.g., minimal/clean, enterprise SaaS, consumer mobile, dark mode). If you have a reference product whose style you like, name it."

**Question 5 — Fidelity**
Ask: "What level of fidelity do you need? (1) Low — rough wireframe with placeholder boxes, (2) Medium — clean layout with real labels and structure, (3) High — pixel-close with realistic content and interactions."

**CRITICAL:** Do not generate mockups until all 5 questions are answered.

---

## Phase 2 — Generate Mockups

For each screen requested, create a separate HTML file named `mockup-[screen-name].html`.

Each file must:
- Be a standalone HTML file (no external dependencies, no CDN links)
- Include all CSS inline in a `<style>` block
- Use real, realistic content — not "Lorem ipsum" or "Button 1"
- Be renderable by opening directly in a browser
- Include navigation between screens where logical (prev/next links or a nav bar)

### Screen Structure Requirements

**Every screen must include:**

1. **Header/Navigation Bar**
   - Product name
   - Current user context (logged in as...)
   - Primary navigation items relevant to the product

2. **Page Title + Context**
   - What page this is
   - Any breadcrumb or back navigation

3. **Primary Content Area**
   - The main UI the user interacts with
   - Realistic data (use plausible fake names, numbers, dates)
   - States: empty state, populated state, loading state (if applicable)

4. **Action Elements**
   - Primary CTA button
   - Secondary actions
   - Any form inputs with appropriate types and placeholder text

5. **Footer or Status Bar** (if relevant)
   - Status indicators, pagination, or summary data

### Fidelity Guidelines

**Low fidelity:**
- Gray boxes for images
- Simple sans-serif font
- Basic layout structure only

**Medium fidelity:**
- Real labels and content
- Clean card-based layout
- Color used only for primary CTAs (single accent color)
- Icons represented as simple shapes or emoji

**High fidelity:**
- Realistic data throughout
- Full color palette (professional, low-saturation)
- Hover states noted in comments
- Micro-copy (button labels, form hints, error messages) written out

---

## Phase 3 — Generate Index Page

Create `mockup-index.html` — a navigation page listing all screens with:
- Screen name
- One-sentence description of what the user does here
- Direct link to the mockup file
- A thumbnail placeholder showing the screen's purpose

---

## Phase 4 — Generate Mockup Brief

Write `mockup-brief.md` containing:

### What Was Built
- List of all screens generated
- Design decisions made and why

### Screen-by-Screen Notes
For each screen:
- **User Goal:** What the user is trying to accomplish
- **Key Interactions:** What can they click/type/do
- **Open Design Questions:** What a real designer would need to decide
- **Content Requirements:** What real data this screen needs

### Next Steps for Design Handoff
- Questions to resolve before sending to a designer
- Components that will need proper design work
- Interactions not represented in static mockups

---

## Rules

- Never use Lorem ipsum — write real product copy
- Every button must have a real label (not "Submit" — use "Analyze Contract", "Save Changes", etc.)
- Show at least one error state or empty state per key screen
- Mockups must be self-contained — they open in any browser with no setup
- If the PRD has success metrics, the mockup should make those metrics visible (e.g., if success = "reduce clicks to complete task", show the minimal flow)
