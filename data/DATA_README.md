# /data — End-to-End Examples (X, y)

This directory explains the thesis project as an **end-to-end AI solution** and provides **50 (X, y) examples**.

## 1) End-to-End Solution

### Inputs (X)
Natural-language requirement artifacts, such as:
- **SRS requirements** ("The system shall ...")
- **User stories**
- **Use-case fragments** (preconditions/steps/postconditions)
- **Change requests / policies / glossary terms** (optional grounding context)

### Processing (AI pipeline)
1. **Data understanding**: parse artifacts and normalize them into requirement statements and candidate pairs.
2. **Defect detection**: identify requirement defects (ambiguity, conflict, incompleteness).
3. **Explainability (XAI)**: produce human-readable reasons and highlight the problematic parts.
4. **Clarity-oriented rewriting**: propose a clearer, verifiable version (e.g., EARS/IEEE-style).
5. **(Optional) SRS assembly**: compile cleaned requirements into an SRS fragment with traceability.

### Outputs (y)
Each output y typically contains:
- defect type (ambiguity / conflict / incompleteness)
- a short explanation ("why it is a defect")
- a proposed clarified rewrite or conflict resolution

## 2) Added value (why this matters)
- **Earlier defect detection** reduces rework and misinterpretation.
- **Clear, verifiable rewrites** convert vague requirements into measurable ones.
- **Traceable explanations** make the result auditable for stakeholder review.

## 3) Files
- `data_examples_xy.csv` — 50 examples in CSV format
- `data_examples_xy.md` — the same 50 examples as a Markdown table
- `DATA_README.md` — this description

## 4) Explanation:

Here’s a simple way to explain it to an audience (or in your GitHub README) without jargon:

### What this data is

This `/data` folder contains **examples that show what my thesis system does from start to finish**.

Each row is one **input-output example** of the system.

### What is **X**

**X = the input requirement text** (or requirement artifact), written in natural language, for example:

* a sentence from an SRS: *“The system shall load quickly.”*
* a user story: *“As a user, I want checkout easily…”*
* a pair of requirements that might contradict each other

So **X is “what a requirements engineer receives”** from stakeholders or existing documents.

### What is **y**

**y = the system’s result**, meaning:

1. it tells you **what defect exists** (ambiguity / incompleteness / conflict),
2. it gives a short **explanation why it is a defect**, and
3. it proposes a **cleaner, testable rewrite** (or a conflict resolution).

So **y is “what a requirements engineer would produce after reviewing and improving X”**, but your AI system does it faster and more consistently.

### Why this matters (added value)

Without the tool, engineers must manually read and fix many requirements.
With your approach:

* vague requirements become **measurable and testable**,
* contradictions are detected early,
* and the output can be directly used to build a **clean SRS**.

### One-sentence summary you can say in a presentation

> “Each example shows how my system takes raw requirements text (X) and outputs detected issues plus a clearer SRS-ready version (y).”
