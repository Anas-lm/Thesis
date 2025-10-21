# End‑to‑End Explanation of the Thesis Solution (with Concrete Data Examples)

**Thesis title (working):** *Application of AI for Optimizing Requirements Specification Processes*

**Core idea:** Build a practical, explainable pipeline that takes **early RE artifacts** (user stories, use cases, change requests, draft SRS) as **inputs**, uses **GPT‑4–based components** (plus lightweight classifiers/rules) as a **black box** to **detect ambiguity & conflicts**, then **generates clarity‑oriented SRS text**, with **traceable explanations** and measurable quality improvements.

---

## 1) End‑to‑End Flow at a Glance

**Inputs → Black‑box system → Outputs**

- **Inputs:**
  - User stories, use cases, change requests, domain glossary/standards, and early SRS fragments.
- **Black box (your solution):**
  1. **Detect**: Ambiguity & conflict detection (GPT‑4 prompts + auxiliary heuristics/classifier for precision).
  2. **Explain**: XAI layer (natural‑language rationales + span highlights + rule hits + references to glossary/standards).
  3. **Generate**: Clarity‑oriented SRS rewriting (pattern‑constrained GPT‑4; EARS/IEEE‑style sentences), then self‑check.
- **Outputs:**
  - **Clean SRS draft** (structured, unambiguous, verifiable) + **Quality Report** (before/after metrics) + **Trace Log** (explanations & provenance).

---

## 2) Data Model & Artifacts (what we feed the system)

**Artifact bundle** `A = {stories, use_cases, change_requests, draft_srs, glossary}`

### Example — Domain: Healthcare Patient Portal

**User stories (US):**
```
US-17: As a patient, I want to view my lab results quickly so that I can understand my status.
US-18: As a clinician, I need immediate access to all patient data during emergencies.
```

**Use case (UC):**
```
UC-05: View Lab Results
Actor: Patient
Preconditions: Patient is authenticated
Main Flow: 1) Patient opens "Lab Results" 2) System displays recent results
Postconditions: Results visible
```

**Change request (CR):**
```
CR-12: Reduce lab results retrieval time from 5s to 2s under normal load.
```

**Draft SRS fragment:**
```
FR-2: The system shall load lab results quickly.
SR-7: During emergencies, all data must be accessible instantly to authorized clinicians.
```

**Glossary/standards (GL):**
```
- "Normal load": < 200 concurrent sessions
- "Emergency mode": declared by triage; access scope limited to allergy, meds, vitals
- "Access control": Role-based; least privilege enforced
```

---

## 3) Black‑Box Stage A — Detection (Ambiguity & Conflict)

### A.1 Ambiguity Detection (per sentence)
**Input:** `FR-2: The system shall load lab results quickly.`

**Model behavior:**
- **Flag:** *Ambiguity: vague adverb* → "quickly"
- **Why:** No measurable threshold; missing load context (normal vs peak); missing data scope.

**XAI rationale (short):**
```
Issue: Unverifiable timing. Term "quickly" is vague.
Evidence: Glossary defines "normal load" but not linked; no time threshold provided.
Recommendation: Add measurable threshold and operating condition.
```

### A.2 Conflict Detection (across artifacts)
**Inputs compared:**
- `US-18: immediate access to all patient data during emergencies.`
- `GL: Emergency mode access limited to allergy, meds, vitals (least privilege).`

**Model behavior:**
- **Flag:** *Conflict: scope of emergency access* (ALL data vs limited set)
- **Why:** User story suggests full data exposure; glossary restricts scope.

**XAI rationale (short):**
```
Issue: Policy conflict. US-18 implies full data; GL restricts to specific categories.
Impact: Privacy/compliance risk (least privilege).
Recommendation: Align US-18 to allowed categories; add audit requirement.
```

---

## 4) Black‑Box Stage B — Explanations (XAI Layer)

For every detection, the system stores a **Trace record**:
```
TRACE {
  input_id: "FR-2",
  issue: "Ambiguity: vague time term",
  spans: ["quickly"],
  rules_triggered: ["vague_adverb"],
  retrieved_context: [GL.normal_load],
  confidence: 0.87,
  suggestion_id: "SUG-441"
}
```
**Human‑readable explanation:**
> *FR‑2 is unverifiable because the term "quickly" lacks a time bound. The glossary defines normal load; recommend specifying a maximum response time under normal load.*

---

## 5) Black‑Box Stage C — Clarity‑Oriented SRS Generation

Generation is **constrained** (EARS/IEEE style) and **grounded** (uses glossary/standards). The system does **not** invent features; it rewrites for clarity and policy alignment.

### C.1 Rewrite — Ambiguity Fix
**Input:** `FR-2: The system shall load lab results quickly.`

**Output (EARS pattern, event‑driven):**
```
FR-2 (Rewritten): When a patient opens the "Lab Results" page under normal load (<200 concurrent sessions),
 the system shall display all available lab results within 2 seconds.
Verification: Load test at 100/150/200 sessions; 95th percentile ≤ 2.0s.
Trace: US-17, UC-05, CR-12, GL.normal_load
```

### C.2 Rewrite — Conflict Resolution
**Inputs:** `US-18` + `GL.policy`

**Output (policy‑aligned):**
```
FR-9 (Emergency Access): When emergency mode is declared by triage,
 the system shall grant clinicians read-only access to allergy, current medications, and vital signs within 1 second,
 with full audit logging of each retrieval.
Security: Role-based access; least privilege enforced.
Trace: US-18, GL.emergency_mode, GL.access_control
```

### C.3 Self‑Check (post‑generation)
- Re‑run detection on outputs; reject if any ambiguity/conflict remains.
- Attach **Verification** blocks to encourage testable requirements.

---

## 6) Outputs (what the stakeholder receives)

### 6.1 Clean SRS Fragment (assembled)
```
2. Functional Requirements

FR-2: When a patient opens the "Lab Results" page under normal load (<200 concurrent sessions),
 the system shall display all available lab results within 2 seconds.
Verification: Load test at 100/150/200 sessions; 95th percentile ≤ 2.0s.
Trace: US-17, UC-05, CR-12, GL.normal_load

FR-9 (Emergency Access): When emergency mode is declared by triage,
 the system shall grant clinicians read-only access to allergy, current medications, and vital signs within 1 second,
 with full audit logging of each retrieval.
Security: Role-based access; least privilege enforced.
Trace: US-18, GL.emergency_mode, GL.access_control
```

### 6.2 Quality Report (Before → After)
```
Document: Patient Portal SRS (v0.3 → v0.4)
- Ambiguity flags: 14 → 3  (−78.6%)
- Conflicts (policy/data scope): 3 → 0
- QUS "Unverifiable" defects: 9 → 1
- Avg. response-time specificity: 21% → 86%
Reviewer satisfaction (Likert 1–5): 2.8 → 4.3
```

### 6.3 Trace Log (excerpt)
```
[TRACE] FR-2: fixed vague timing → added 2s bound; grounded in GL.normal_load; verified via CR-12.
[TRACE] FR-9: resolved scope conflict → aligned to least-privilege categories; added audit requirement.
```