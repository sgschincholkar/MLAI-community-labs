# Module 2 — Commands, Context & Market Research

Build a reusable PM command library and run a full research-to-PRD workflow — market research, user research, and a structured PRD — all on the same feature.

---

## Lessons

| # | Lesson | What You'll Do |
|---|--------|---------------|
| 2.1 | [Slash Commands in Claude Code](./Lesson2.1-Slash-Commands-in-Claude-Code.md) | Understand how built-in and custom slash commands work |
| 2.2 | [Custom Slash Commands](./Lesson2.2-Custom-Slash-Commands.md) | Build `/market-research`, `/user-research`, and `/prd` commands |
| 2.3 | [Market Research — Chaining Prompts](./Lesson2.3-Chaining-Research-Prompts.md) | Chain 4 research stages on the Lease Compliance feature, update CLAUDE.md |
| 2.4 | [User Research — Chaining Prompts](./Lesson2.4-User-Research-Chaining.md) | Chain user research on the same feature using market research as context |
| 2.5 | [PRD](./Lesson2.5-PRD.md) | Turn both research outputs into a structured PRD, update CLAUDE.md |

---

## The Chain

Every lesson builds on the same feature — Lease Compliance Reporting for LegalGraph:

```
2.3 → market-research-lease-compliance-<date>.md
2.4 → user-research-lease-compliance-<date>.md  (uses 2.3 as context)
2.5 → prd-lease-compliance-<date>.md            (uses 2.3 + 2.4 as context)
```

---

## What You'll Have by the End

- Three reusable slash commands in your personal library
- Three research output files saved in `outputs/`
- CLAUDE.md updated with market intelligence, user research, and PRD decisions

---

*Previous: [Module 1 — Claude Foundation](../Module-1%20-%20ClaudeFoundation/README.md)*
*Next: [Module 3 — Prototype, Connect & Automate](../Module-3%20-%20Prototype%2C%20Connect%20%26%20Automate/README.md)*
