Here’s a clean **end-to-end presentation** you can use in your thesis + GitHub to explain the whole idea, with **X → (AI pipeline) → y**, and clearly stating **all your contributions (A+B+C)**.

---

# End-to-End AI Solution for Optimizing Requirements Specification

## 1) The problem (why we need this)

In real projects, requirements are written in natural language across multiple artifacts (user stories, use cases, change requests, SRS drafts). These texts often contain defects such as:

* **Ambiguity** (“quickly”, “secure”, “user-friendly”) → multiple interpretations
* **Incompleteness** (missing triggers/conditions/metrics) → not testable
* **Conflicts** (contradicting rules across documents) → incorrect implementation

These defects cause rework, misunderstandings, and delayed validation.

---

## 2) End-to-end system view

### Input (X)

**X is any requirement artifact**, or a bundle of artifacts, for example:

* a single SRS sentence
* a user story
* a use case step
* a pair of requirements (for conflict checking)
* a “bundle” containing stories + use cases + policies/glossary + SRS draft

**Example X (bundle):**

* User story: “As a patient, I want to view lab results quickly.”
* Draft SRS: “The system shall load lab results quickly.”
* Change request: “Reduce retrieval time from 5s to 2s.”
* Glossary: “Normal load < 200 concurrent sessions.”

---

### Black box processing (your AI pipeline)

Your system processes X through a full pipeline:

1. **Data understanding**

   * Parse artifacts, split into requirement candidates, assign IDs, build candidate pairs for conflict checks.

2. **Defect detection (AI/ML + rules)**

   * Detect **ambiguity** (vague terms, unclear references, unverifiable statements)
   * Detect **incompleteness** (missing actor/condition/metrics)
   * Detect **conflicts** (contradiction between two requirements or two artifacts)

3. **Explainability (XAI)**

   * For each issue, provide:

     * defect type
     * why it was flagged
     * which words/spans triggered it
     * confidence score
     * trace links back to the original artifact(s)

4. **Clarity-oriented rewriting (guardrailed generation)**

   * Generate refined requirements using structured patterns (EARS/IEEE style)
   * Add **measurable constraints** only when grounded by input (CR/policy/glossary) or mark “needs stakeholder decision”
   * Prevent hallucination (“do not introduce new features”)

5. **SRS assembly**

   * Compile the cleaned requirements into an SRS fragment/document
   * Include verification hints + traceability matrix + quality report

---

### Output (y)

**y is what the system produces**, for example:

* list of detected defects + explanations
* cleaned rewritten requirements
* an SRS-ready fragment with verification + traceability
* a quality report (before vs after)

**Example y (simplified):**

* Defect: ambiguity (“quickly”) → unverifiable timing
* Rewrite: “When a patient opens ‘Lab Results’ under normal load (<200 sessions), the system shall display results within 2 seconds (P95).”
* Verification: load test
* Trace: US-17, CR-12, GL-normal_load

---

## 3) One simple example (X → y)

### X (raw requirement)

“The system shall respond in real time.”

### y (system output)

* **Defect detected:** Ambiguity (“real time” undefined)
* **Explanation:** timing not measurable → not verifiable
* **Proposed rewrite:**
  “The system shall deliver sensor readings to the UI within 250 ms end-to-end latency.”
* **Verification:** latency test with 95th percentile ≤ 250 ms

---

## 4) Your contributions (ALL options included)

### Contribution A — Integrated end-to-end pipeline (not a single-task tool)

Most existing tools focus on only one task (detect ambiguity, or classify, or generate).
**Your system integrates detection + explanation + rewriting + SRS assembly** into one workflow.

**Added value:** real process optimization, not isolated NLP.

---

### Contribution B — Cross-artifact conflict detection (“real world conflicts”)

Conflicts often exist **between** artifacts:

* user story vs glossary/policy
* use case vs SRS
* change request vs older requirement

Most tools check single sentences inside one SRS document only.

**Added value:** detects defects earlier (“shift-left”), before SRS freeze.

---

### Contribution C — Guardrailed clarity-oriented generation

LLM-based generation exists, but outputs can be:

* fluent but unverifiable
* inconsistent
* hallucinated

Your approach uses:

* structured patterns (EARS/IEEE style)
* grounding (glossary/policies)
* self-check loop (reject if still defective)
* traceability log (audit trail)

**Added value:** safer, more testable rewriting that stakeholders can trust.

---

### Contribution D — Measurable quality improvement framework

Not just accuracy. You measure:

* defect reduction (ambiguity/conflict/unverifiable)
* ISO 29148 / QUS rubric improvements
* time-to-review improvement
* usefulness of explanations (expert rating)

**Added value:** proves “optimization” with evidence.

---

### Contribution E — Reusable dataset + prompt assets for RAG

You provide:

* `/data` (X,y) examples (50 now, scale to 1,000+)
* `/prompts` (zero-shot + few-shot)
* retrieval step (ChromaDB) to improve performance

**Added value:** reproducibility + future extensibility.

---

## 5) briefly

> “My system takes messy natural-language requirements (X), detects and explains ambiguity/conflicts, rewrites them into verifiable structured requirements, and outputs an SRS-ready document (y) with traceability and measurable quality improvement.”

---

## 6) added value

Without the tool: engineers manually read and rewrite many requirements → slow, inconsistent.
With the tool:

* problems are found early
* fixes are suggested in standard format
* stakeholders can audit the reasoning
* quality improves in measurable ways
