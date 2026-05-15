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