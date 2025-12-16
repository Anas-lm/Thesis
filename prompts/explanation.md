You should understand that this task is basically asking you to **prove your thesis idea as a single “AI agent” product**, not just a thesis text.

In simple terms, they want three things:

## 1) Your thesis as an end-to-end mapping

You must be able to say clearly:

* **X** = the raw input (requirements artifacts: user stories / use cases / SRS sentences / policies)
* **Agent** = one AI system that handles everything (detect → explain → rewrite → assemble)
* **y** = the final output (defect report + refined requirements + SRS-ready result)

So the agent is treated like a black box:
**Give it X → it returns y**.

## 2) Prompts are your “program”

They want your agent to be implemented (at least conceptually) using **prompt engineering**.

That’s why you must create `/prompts/` in GitHub:

* it acts like documentation of how your AI agent works
* it shows the exact instructions that make the AI behave as your end-to-end pipeline

## 3) You must show two ways the agent can work

### Prompt 1 (zero-shot)

One new input X → agent returns y.
This shows your agent can work **without examples**, just from instructions.

### Prompt 2 (few-shot)

You give the agent several known **(X, y)** examples first (from your `/data` table), then a new X.
This shows that by giving examples, the agent can behave more consistently and accurately.

**Key idea:** few-shot prompting = using your dataset as “teaching examples” inside the prompt.

---

### What the teacher expects as a final deliverable

* A GitHub folder `/prompts/` containing:

  * Prompt 1 file (zero-shot)
  * Prompt 2 file (few-shot)
  * (optional) README explaining X and y

And in your report/presentation:

* explain the agent as:

  * Input X → stages inside agent → Output y
* show outputs produced by both prompts

---

### One sentence summary

> “This task is about packaging my thesis system as one AI agent and demonstrating it through prompts: zero-shot and few-shot, where X is raw requirements and y is detected defects + refined SRS-ready requirements.”
