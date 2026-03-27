 engineering
# Copilot Instructions – Project Context Enforcement

## Objective
Ensure all generated outputs (e.g., feature expansion, test cases, code) are strictly grounded in project context and knowledge assets, while avoiding hallucination.

---

## Core Principles

### 1. Knowledge-First Approach
- Always prioritize information from the **knowledge assets folder**.
- Treat knowledge assets as the **single source of truth**.
- Do not generate assumptions if relevant data exists in knowledge assets.

---

### 2. No Hallucination Policy
- Do NOT invent:
  - Requirements
  - APIs
  - Data structures
  - Business logic
- If information is missing:
  - Clearly state: *"Insufficient context from knowledge assets"*
  - Do NOT fill gaps with assumptions

---

### 3. Context Loading
- Before executing any command:
  - Read and understand all relevant files from the **knowledge assets folder**
  - Extract:
    - Business context
    - Functional requirements
    - Dependencies
    - Constraints

---

### 4. Command Execution Standard
For any command (e.g., `generate feature expansion v2`):

- Ensure:
  - Output aligns with knowledge assets
  - No deviation from defined requirements
  - No generic or template-based responses unless justified

---

### 5. Output Quality Guidelines
- Be:
  - Precise
  - Context-aware
  - Structured
- Avoid:
  - Generic filler content
  - Repetition
  - Assumptions beyond given data

---

### 6. Conflict Handling
- If there is conflicting information:
  - Highlight the conflict
  - Prefer the most recent or authoritative source
  - Do not merge conflicting logic silently

---

### 7. Traceability (Very Important)
- Wherever possible:
  - Reference which part of knowledge assets influenced the output
  - Maintain logical traceability between input and output

---

## Example Execution Instruction

When executing:
`generate feature expansion v2`

Follow this flow:
1. Load knowledge assets
2. Understand story context
3. Validate completeness
4. Generate expansion strictly based on available data
5. Flag missing or ambiguous areas explicitly

---

## Strict Rule
> If it is not in knowledge assets or explicitly provided context, DO NOT assume it.