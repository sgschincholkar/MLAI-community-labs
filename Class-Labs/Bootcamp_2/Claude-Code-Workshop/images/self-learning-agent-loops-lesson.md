# Lesson: Self-Learning Agent Loops — The Ralph Loop & AutoResearch

*Prepared for: Rajat (LegalGraph)*
*Date: April 18, 2026*

---

## 1. What You Will Learn

By the end of this lesson you will understand:

1. What a **self-learning agent loop** is and why it works.
2. The **Ralph Loop** (a.k.a. Ralph Wiggum Loop) — the simplest possible persistent-agent pattern.
3. **AutoResearch** — Andrej Karpathy's loop for autonomous ML research.
4. The three structural primitives every self-learning loop needs.
5. When to reach for these patterns (and when NOT to).
6. A practical recipe you can try today.

---

## 2. The Core Intuition

LLM agents are extremely capable *for a single turn* but forget everything when the context window closes. The self-learning loop turns that weakness into a strength by moving "memory" **out of the context window and onto disk**.

> *"Progress doesn't persist in the LLM's context window — it lives in your files and git history."*

Each loop iteration:

1. Starts with a **fresh context** (cheap, clean, no drift).
2. Reads the **state-of-the-world** from disk (specs, plan, prior diffs, test output, metric logs).
3. Takes **one small action** (edit a file, run a test, propose an experiment).
4. Leaves a **durable artifact** (commit, log, updated plan) for the next iteration to learn from.

The "learning" isn't gradient-based — it's *systematic accumulation of outcomes* that future iterations condition on. Brute-force persistence + a good feedback signal = surprisingly strong compounding improvement.

---

## 3. The Ralph Loop

### 3.1 Origin

- Coined by **Geoffrey Huntley** in July 2025 in the post *"Ralph Wiggum as a 'software engineer'"*.
- Named after the Simpsons character — the joke is that a naive, persistent agent ("I'm in danger!") outperforms elaborate agentic architectures.
- Went viral in December 2025 / January 2026 once Anthropic shipped an official **Ralph Wiggum plugin** for Claude Code using stop-hooks.

### 3.2 The Original One-Liner

```bash
while :; do cat PROMPT.md | npx --yes @sourcegraph/amp ; done
```

That's it. A `while true` that re-feeds the same prompt to a coding agent forever. The agent sees the current state of the repo on each iteration, fixes what's broken, commits, and the loop restarts.

### 3.3 Canonical Pseudocode

```
while not done:
    read IMPLEMENTATION_PLAN.md
    pick next incomplete task
    implement it
    run tests / linters
    if all pass:
        commit
        mark task done in plan
        emit <promise>DONE</promise>
    else:
        exit — next iteration retries with a fresh context
```

### 3.4 Why It Works

- **Fresh context each iteration** avoids the lossy-compaction failure mode that kills long-running single-session agents.
- **Git + plan file = durable memory.** The agent "learns" by reading diffs and remaining TODOs.
- **Tests are the reward signal.** Failing tests apply backpressure; passing tests lock in progress.
- The agent never needs to hold the whole project in its head — only the next micro-task.

### 3.5 When To Use

- Multi-step coding work with **testable acceptance criteria**.
- Mechanical, well-defined tasks (migrations, lint-sweeps, CRUD wiring, refactors).
- When you want to run agents for **hours**, not minutes, unattended.

### 3.6 When NOT To Use

- Tasks requiring **judgment calls** or ambiguous requirements.
- Work where there is no automatic verifier (no tests, no metric).
- Anywhere unsupervised writes are unsafe (prod infra, untested migrations).

### 3.7 Pitfalls

- **Weak specs → infinite retries.** Ralph will happily loop forever on a vague goal.
- **No exit criterion.** Require an explicit `EXIT_SIGNAL` or "promise" the agent must emit.
- **Cost runaway.** Set `--max-iterations` and a budget cap.
- **Silent regressions.** Make sure tests actually cover what you care about — Ralph optimizes for what you measure.

---

## 4. AutoResearch (Karpathy's Loop)

### 4.1 Origin

- Released by **Andrej Karpathy** in March 2026 as a ~630-line Python script.
- Ran **50 experiments overnight** on a single GPU without human input, tuning a nanochat training script.
- **Tobi Lütke (Shopify CEO)** publicly reported a **19% performance gain after 37 overnight experiments** on internal data.

### 4.2 The Three Primitives

AutoResearch formalizes what Ralph does informally:

| Primitive          | Ralph Loop             | AutoResearch                          |
| ------------------ | ---------------------- | ------------------------------------- |
| **Editable asset** | `src/` code + `plan.md` | `train.py` (single file)              |
| **Scalar metric**  | tests pass/fail        | `val_bpb` (validation bits-per-byte)  |
| **Time-boxed cycle** | "until done"         | Fixed 5-minute training budget        |

Two rules worth memorizing:

1. **One editable asset.** Confining edits to one file keeps every hypothesis reviewable as a diff.
2. **One scalar metric.** Must be computable without human judgment and unambiguous about direction.

### 4.3 The Loop

```
loop:
    propose code edit to train.py
    run training for fixed wall-clock budget (e.g. 5 min)
    measure val_bpb
    if val_bpb improved:
        keep change, log trajectory
    else:
        revert
    update internal policy from trajectory
```

The agent's "learning" is an accumulating **trajectory of experiment outcomes** that conditions subsequent proposals — effectively online in-context meta-learning.

---

## 5. Ralph vs. AutoResearch — Side by Side

| Dimension          | Ralph Loop                          | AutoResearch                          |
| ------------------ | ----------------------------------- | ------------------------------------- |
| Domain             | Software engineering tasks          | ML experimentation                    |
| Feedback signal    | Tests / lint                        | Validation metric                     |
| Memory             | Git + plan file                     | Trajectory log + frozen environment   |
| Termination        | Plan complete OR `EXIT_SIGNAL`      | Budget exhausted OR convergence       |
| Reward granularity | Binary (pass/fail)                  | Continuous (scalar)                   |
| Best at            | Shipping code                       | Discovering better configurations     |

The shared DNA: **one editable surface, one measurable signal, one repeating cycle.**

---

## 6. Designing Your Own Self-Learning Loop — A Checklist

Before writing any code, answer these six questions:

1. **What single file / artifact is the agent allowed to modify?**
   (If you can't name it, the loop will thrash.)
2. **What single number tells you whether an iteration was better?**
   (Tests pass count, accuracy, latency, cost — pick one.)
3. **What is the maximum per-iteration budget?**
   (Wall-clock, tokens, dollars.)
4. **What is the stop condition?**
   (Metric plateau, explicit signal, iteration cap.)
5. **Where does durable memory live?**
   (Git history, append-only log, plan file.)
6. **What is the fallback if the loop goes off the rails?**
   (Hard kill switch, cost alarm, branch isolation.)

If any of these is fuzzy, your loop will be fuzzy.

---

## 7. A Starter Recipe You Can Run Today

**Use case:** self-healing test suite. The agent fixes failing tests until the suite is green.

```bash
#!/usr/bin/env bash
# ralph.sh — minimal Ralph loop
MAX_ITER=20
i=0
while [ $i -lt $MAX_ITER ]; do
  # 1. Check the world
  if npm test --silent; then
    echo "DONE at iteration $i"
    exit 0
  fi

  # 2. Give the agent ONE focused task
  claude -p "Read the latest test output in test-output.log. \
             Fix ONE failing test. Commit with a clear message. \
             Then exit."

  # 3. Capture durable state
  npm test > test-output.log 2>&1 || true
  git log --oneline -1

  i=$((i+1))
done

echo "Hit iteration cap. Review manually."
```

Notice how this hits all six checklist items: the editable asset is the repo, the metric is `npm test` exit code, the budget is 20 iterations, the stop condition is a green suite, memory lives in git + `test-output.log`, and the fallback is the iteration cap.

---

## 8. Applying This at LegalGraph

A few places this pattern could pay off immediately:

- **Contract-extraction eval loop.** Editable asset = your extraction prompt / rules file. Metric = F1 on a held-out labeled set. Time-box = N documents. Run overnight; wake up to a better extractor.
- **Clause-classifier tuning.** Same pattern, metric = classification accuracy.
- **Doc-ingestion pipeline hardening.** Metric = % of real client documents that parse end-to-end without error.
- **Self-healing CI.** Ralph loop over your test suite on every failing PR branch.

The common thread: anywhere you have a **labeled eval set or automatic verifier**, you can put an agent in a loop and let it compound improvements while you sleep.

---

## 9. Key Takeaways

1. Self-learning agent loops work by **moving memory to disk** and using **fresh contexts** every iteration.
2. The **Ralph Loop** is the engineering flavor: plan file + tests + git history.
3. **AutoResearch** is the research flavor: one file + one scalar + one time budget.
4. Both reduce to: **one editable surface, one signal, one cycle.**
5. The hard part is not the loop — it's **defining the metric** and the **stop condition**.
6. Naive persistence + a clean feedback signal beats elaborate agent architectures in most practical settings.

---

## 10. Further Reading

- Geoffrey Huntley — [Ralph Wiggum as a "software engineer"](https://ghuntley.com/ralph/)
- Geoffrey Huntley — [Everything is a Ralph Loop](https://ghuntley.com/loop/)
- Anthropic — [Ralph Loop plugin for Claude Code](https://claude.com/plugins/ralph-loop)
- Anthropic — [Ralph Wiggum plugin README](https://github.com/anthropics/claude-code/blob/main/plugins/ralph-wiggum/README.md)
- Andrej Karpathy — [autoresearch (GitHub)](https://github.com/karpathy/autoresearch)
- The New Stack — [Karpathy's 630-line script ran 50 experiments overnight](https://thenewstack.io/karpathy-autonomous-experiment-loop/)
- Fortune — [Why everyone is talking about Karpathy's autonomous AI research agent](https://fortune.com/2026/03/17/andrej-karpathy-loop-autonomous-ai-agents-future/)
- Addy Osmani — [Self-Improving Coding Agents](https://addyosmani.com/blog/self-improving-agents/)
- HumanLayer — [A Brief History of Ralph](https://www.humanlayer.dev/blog/brief-history-of-ralph)
- The Register — [Ralph Wiggum loop prompts Claude to vibe-clone software](https://www.theregister.com/2026/01/27/ralph_wiggum_claude_loops/)
- AutoResearch-RL paper — [arXiv 2603.07300](https://arxiv.org/abs/2603.07300)
