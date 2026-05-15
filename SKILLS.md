# 🛠️ AIDD Skills: Prompt Engineering Standard (Anthropic Best Practices)

This document establishes the technical standards for constructing highly deterministic, production-grade prompts (optimized for the Claude model family) to minimize variance and maximize code precision [00:00:20].

## 📐 1. Production Prompt Anatomy (Single-Turn Execution)
Within structured development environments (IDEs, project knowledge contexts), we minimize conversational chatting and aim for first-time right execution [00:04:12]. Build advanced prompts using this explicit hierarchy [00:04:29]:

1. **Task Context:** Define the role and objective (e.g., *"You are an elite software architect..."*) [00:04:29].
2. **Tone Context:** Instruct the model to be objective and fact-driven. If information is missing, it must throw an error, not guess [00:06:04].
3. **Static Background Data:** System architecture maps, AIDD repository files, and core module metadata [00:08:58].
4. **Dynamic Input:** The specific target code, Jira ticket, or feature sketch [00:04:34].
5. **Detailed Instructions:** A strict step-by-step algorithm for the AI to follow [00:04:51].
6. **Few-Shot Examples:** Ideal input-output structural pairs [00:04:56].
7. **Immediate Reminder:** Reiterate critical constraints at the very end of the prompt window [00:05:08].

## 🏷️ 2. Structural Separation via XML Tags
Claude models are natively trained to handle complex context using XML formatting [00:10:15, 00:14:34].
* **The Rule:** Always wrap distinct blocks of data in explicit XML structures (e.g., `<source_code>`, `<specifications>`, `<instructions>`) [00:10:21].
* **The Why:** This blocks prompt-injection attacks (where user input accidentally overwrites core system guidelines) and allows the model to precisely reference target blocks during its reasoning process [00:10:33].

## 💾 3. Prompt Caching Strategy
* **The Rule:** Keep all highly static documents (such as DB schemas, core framework conventions, and these AIDD rulebooks) stored within the persistent **System Prompt** layer [00:10:51].
* **The Why:** This triggers *Prompt Caching* [00:09:23]. On subsequent calls, the engine bypasses re-analyzing static data, speeding up response times drastically and slashing input token expenses by up to 90% [00:09:28].

## 🔄 4. Ordering of Analysis (Enforced Thinking Steps)
LLMs struggle when forced to solve a multi-layered problem and output the solution simultaneously [00:02:47]. High accuracy requires enforcing a logical analysis pipeline [00:17:28].
* **The Protocol:** When requesting code changes, force the model to output a factual critique first within hidden `<thinking_scratchpad>` or `<code_analysis>` tags *before* it generates a single line of actual code [00:18:08, 00:19:30].

## ⚙️ 5. Pre-filling & Output Constraints
* **The Rule:** When an automated script or tool requires clean JSON or raw code blocks without conversational filler text ("Here is your code..."), leverage the *Pre-filling* technique [00:20:28, 00:22:16].
* **Execution:** Manually initialize the model’s response block with the first expected characters, such as `{` or an opening `<json>` tag, forcing the model to instantly stream compliant data [00:21:15, 00:22:52].