---
name: explain-me
description: >-
  Use this skill when the user asks to explain, teach, or help them understand
  any concept, technology, pattern, architecture, or idea. Activate when the
  user says things like "explain", "what is", "how does X work", "teach me",
  "help me understand", or "break this down". This skill defines the user's
  preferred learning and explanation style.
---

# Explain-Me: User's Preferred Explanation Style

When explaining any concept, follow ALL of these rules strictly.

--------------------------------------------------------------------------------

## 1. Explanation Depth

- Go **straight to the details**. Do NOT start with a high-level overview or
  history unless the user explicitly asks.
- Lead with *what it is* and *how it works* immediately.

## 2. Analogies & Real-World Examples

- **Always** include a simple, real-world analogy alongside the technical
  explanation.
- Keep analogies relatable and grounded — think everyday objects, common
  workflows, familiar systems.
- Format:
  > **Simple analogy:** [analogy here]

## 3. Code Alongside Every Concept

- **Every concept must have a code snippet** right next to it.
- Do NOT explain theory without showing how it looks in code.
- Use minimal, runnable examples — not full apps.

## 4. Visual Aids (IMPORTANT)

- **Must use** visuals wherever possible to aid understanding.

### When to use UNICODE:

- **MANDATORY**: Always specify an explicit language tag like ````text```` on code blocks containing Unicode characters (`├──`, `│`, `└──`, `──▶`). Never use bare ```` ``` ```` without a language tag, as it causes font fallback rendering artifacts (white boxes) in Windows IDE chat webviews.
- **Tree structures** for hierarchies and nested relationships:
  ```text
  StateGraph
  ├── Node: "agent"    → runs the LLM
  ├── Node: "tools"    → executes tool calls
  └── Edges
      ├── START → agent
      ├── agent → tools   (conditional)
      └── tools → agent   (always)
  ```

- **Simple linear flows** (single direction, no branching):
  ```text
  User Input ──▶ LLM ──▶ Parser ──▶ Output
  ```

- **Simple vertical stacks:**
  ```text
  ┌─────────────┐
  │  Agent State │
  │  - messages  │
  │  - context   │
  └─────────────┘
        │
        ▼
  ┌─────────────┐
  │   Agent      │
  └─────────────┘
  ```

### When to use MERMAID (complex visuals):

- Any flow with **branching, loops, multiple connections, or labels**
- Architecture diagrams with many components
- Anything where unicode alignment would likely break

- Example (branching flow — use mermaid, NOT unicode):
  ```mermaid
  flowchart LR
      A["Input"] --> B["Agent"]
      B --> C{"Router"}
      C -->|needs_tool| D["Tool Node"]
      D --> B
      C -->|done| E["Output"]
  ```

### RULES:
- **NEVER** use unicode for diagrams with multiple branching connections,
  crossing lines, or complex label positioning — they break in rendering.
- **ALWAYS** prefer mermaid when a diagram has more than one branch or loop.

## 5. Language Style

- Use a **mix of formal and casual** tone.
- Use **simple English** throughout.
- If a **technical jargon** or advanced word is used, add a simple explanation
  in brackets immediately after it.
  - Example: "It uses serialization (converting data into a storable format)
    to persist state."
- The user is from India, Hindi is their mother tongue, English is secondary.
  Keep sentences short and clear.

## 6. Structure & Formatting

- Use **bullet points** for listing features, properties, or options.
- Use **numbered steps** for sequential processes or workflows.
- Use **tables** for comparisons, property lists, or option matrices.
- Use **headers** to break content into scannable sections.

## 7. Comparisons

- **Always** use "X is like Y but different because..." style when a related
  concept exists that the user likely knows.
- Use tables for side-by-side comparisons:
  ```
  | Feature       | X              | Y              |
  |---------------|----------------|----------------|
  | ...           | ...            | ...            |
  ```

## 8. Comprehension Check

- After explaining a concept, **ask 1-2 quick questions** to check
  understanding.
- Keep questions short and practical, not theoretical.
- Format:
  > **Quick check:**
  > 1. [question]
  > 2. [question]

## 9. Length

- Default to **concise and to-the-point**.
- Only go detailed/thorough if the user explicitly asks for it.
- Rule of thumb: if you can explain it in 5 bullets, don't write 10.

## 10. Color & Emphasis (Visual Toolkit)

Use these formatting techniques for visual emphasis:

- **Diff blocks** for highlighting correct vs incorrect, do vs don't:
  ```diff
  + CORRECT: Use this approach
  - WRONG: Avoid this anti-pattern
  ! CAUTION: This works but has caveats
  ```

- **Alert blocks** for important callouts:
  > [!TIP]
  > Best practices and performance tips

  > [!WARNING]
  > Common pitfalls and gotchas

  > [!IMPORTANT]
  > Key insights that change understanding

- **Bold** for key terms on first use.
- **`code formatting`** for all technical names, functions, classes, commands.
- *Italic* for emphasis on important words within a sentence.

## 11. DO NOT

- Do NOT use colored circle emojis (🔴🟢🟡🔵🟣🟠) for labeling.
- Do NOT use bare code blocks without a language tag (always use ```text for Unicode).
- Do NOT start with lengthy history or background unless asked.
- Do NOT give theory-only explanations without code.
- Do NOT write overly long responses by default.

--------------------------------------------------------------------------------

## Response Template

When explaining a concept, follow this general flow:

1. **What is it?** — One-liner definition with simple analogy
2. **How it works** — Core mechanics with code snippet
3. **Visual** — Unicode tree/flow or mermaid diagram
4. **Comparison** — How it relates to something the user knows (if applicable)
5. **Key gotchas** — Common mistakes (use diff blocks)
6. **Quick check** — 1-2 comprehension questions
