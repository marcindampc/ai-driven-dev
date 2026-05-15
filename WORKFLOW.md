# 🔄 Development Lifecycle: Spec-Driven Development (SDD)

To ensure that AI-assisted outputs are reliable, predictable, and robust, it is strictly forbidden to jump directly into code generation without prior planning. Every feature or modification must pass through the following iterative SDD loop.

## 🛠️ Step-by-Step SDD Loop

### Step 1: Research & Bounded Context (Domain Isolation)
* Before writing a prompt, identify the precise business domain, sub-domain, or bounded context you are working within.
* **Architectural Guideline:** In the age of AI, Domain-Driven Design (DDD) principles and strong modular encapsulation are more vital than ever. Isolating logic into autonomous, decoupled modules protects the system from aggregate bloat and enables the LLM to generate highly accurate changes within restricted scopes.

### Step 2: Plan (Architecting the Change)
* Force the LLM to output a purely textual architectural blueprint/plan before it is allowed to touch or modify any code files.
* The plan must explicitly define: where the new logic hooks into, which files will be modified, and whether database/schema changes are required.

### Step 3: Criteria & Specification (Defining Boundaries)
* Establish precise technical specifications and strict acceptance criteria, including edge cases and negative flows.
* The ultimate validation of intent is forcing the AI to concurrently generate unit or integration tests based strictly on the provided specification.

### Step 4: Implementation (Granular Execution)
* Execute code generation in small, isolated, and highly controlled increments.
* Avoid massive, open-ended prompts like "write this entire module." Direct the AI to implement specific, targeted logic blocks.

### Step 5: Verification (Code Review)
* Conduct a rigorous post-generation review adhering strictly to the code verification rules detailed in `AGENTS.md`.
* Apply the **Zero Unexplained Lines** rule: every block of AI-generated code must be explainable by the human reviewer before it is merged. If you cannot articulate *why* a specific approach was chosen, reject the block and regenerate with a stricter prompt.
* Force a secondary self-audit by the LLM: prompt it to re-examine its own output for performance anti-patterns, hidden coupling, and edge-case gaps before you begin your own review.

### Step 6: Documentation & Auditability
* **Log Intent, Not Conversations:** Do not commit raw chat transcripts. Instead, document the *core instruction template* used to generate a significant module — either in the commit message or a short inline comment block.
* **Prompt Versioning:** If a feature required a complex multi-step prompt structure, preserve that structure in the relevant commit message so the same context can be reconstructed when the module needs to be extended in the future.
* **Commit Discipline:** Each commit should represent one complete SDD cycle iteration. The commit message should answer: *what changed, why this approach, and which AI-assisted decisions were made.*

---

## 🔁 The Iterative Loop

The SDD loop is not strictly linear. Verification failures at **Step 5** should route back to the appropriate upstream step:

| Failure Type | Route Back To |
|---|---|
| Logic does not match specification | Step 3 — redefine criteria |
| Architectural approach is flawed | Step 2 — revise the plan |
| Scope is unclear or too large | Step 1 — re-isolate the bounded context |
| Output is correct but unauditable | Step 4 — regenerate in smaller increments |