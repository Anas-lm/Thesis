# Prompts — ReqOpt-Agent (End-to-End AI Requirements Optimization)

## Goal
These prompts demonstrate the thesis system as a single end-to-end AI agent:
Input X (requirements artifacts) → detect defects + explain + rewrite → output y (SRS-ready results).

## Expected Input (X)
X is a text bundle containing any mix of:
- User stories
- Use cases
- Change requests
- Draft SRS requirements
- Glossary/policies (optional)

## Expected Output (y)
The agent returns a single JSON object with:
- detections[] (defect type, spans, confidence, rationale, related IDs)
- rewrites[] (EARS/IEEE rewrite + verification hint + trace)
- srs_fragment (assembled clean fragment)
- notes (warnings: “needs stakeholder decision”, missing thresholds, etc.)

## Constraints
- Do NOT invent new functionality not present in X.
- Only introduce numeric thresholds if they are provided in X (CR/Policy/Glossary).
- If a value is missing, mark: "needs stakeholder decision".
- Keep outputs verifiable (testable).
