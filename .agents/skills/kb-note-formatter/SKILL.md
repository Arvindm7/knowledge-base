---
name: kb-note-formatter
description: >-
  Converts raw text, course transcripts, or unstructured explanations into standardized,
  production-ready Markdown notes matching the knowledge-base repository style.
  Use when the user provides raw text or lecture notes and asks to create or format a note file.
---

# Knowledge Base Note Formatter Skill

This skill defines the standardized structure, formatting guidelines, and workflow for converting raw text, course notes, lecture transcripts, or concept explanations into high-quality `.md` files for the `knowledge-base` repository.

---

## 1. File Naming & Directory Conventions

Always verify existing files in the target directory to determine the correct numerical prefix and naming pattern:

- **Naming Pattern:** `XX.topic-name.md` (e.g., `01.intro.md`, `02.class-and-objects.md`, `19.solid-principles.md`).
- **Target Directories:**
  - `Object Oriented Programming/` — Fundamental and advanced OOP concepts.
  - `Low Level Design/` — System design patterns, UML, schema design, and modular architecture.
  - `JAVA/` — Core Java language concepts, syntax, APIs, JVM internals, and libraries.
- **Rules:**
  - Lowercase with hyphens for multi-word topic names (e.g., `14.relationships-between-classes.md`).
  - Maintain two-digit sequence prefixes (`01`, `02`, ..., `10`, etc.).

---

## 2. Standard Note Anatomy

Every note in this knowledge base must adhere to the following section hierarchy:

```markdown
# <Topic Title in Title Case>

> <Concise, punchy quote, definition, or one-sentence thesis statement>

## What You'll Learn

By the end of this chapter, you'll understand:

- <Core learning objective 1>
- <Core learning objective 2>
- <Core learning objective 3>
- <Core learning objective 4>

---

## <Concept 1: Definition & Overview>

<Clear explanation of the concept, breaking down jargon into intuitive terms.>

<Include a Mermaid diagram here if the concept involves relationships, flow, or architecture.>

---

## <Concept 1 — Real-Life Analogy>

<Intuitive real-world analogy (e.g., house construction, banking system, car manufacturing).>

---

## <Concept 2: Technical Deep Dive & Java Code Implementation>

<Detailed explanation of technical mechanisms, rules, and lifecycle.>

```java
// Clean, idiomatic Java code with clear inline comments
import java.util.*;

public class Example {
    // Attributes with access modifiers
    private String name;

    // Constructors
    public Example(String name) {
        this.name = name;
    }

    // Methods with proper encapsulation
    public void execute() {
        System.out.println("Executing: " + name);
    }
}
```

---

## <Concept 3: Comparison / Deep Breakdown>

| Aspect | <Concept A> | <Concept B> |
| :--- | :--- | :--- |
| **Definition** | ... | ... |
| **Approach** | ... | ... |
| **Use Case** | ... | ... |

---

## Summary

| Concept / Aspect | Key Takeaway |
| :--- | :--- |
| **<Topic A>** | <Summary takeaway> |
| **<Topic B>** | <Summary takeaway> |
```

---

## 3. Formatting & Styling Guidelines

### Typography & Headings

> [!IMPORTANT]
> **TOC Compatibility Rule:** The right-side Table of Contents in the IDE only renders `##` (H2) and `###` (H3) headings. To ensure every major section and sub-topic is clickable and visible in the TOC, follow these strict heading rules:

- Use a **single `#`** for the main file title only — this is NOT shown in the TOC.
- Use **`##`** for every top-level navigable section (concept introductions, code examples, comparisons, analogies, benefits, caveats, summaries, etc.).
- Use **`###`** sparingly — only for minor clarifications or labeled sub-points *within* a `##` section that don't need their own TOC entry.
- **Never use `####` (H4) headings** — they are invisible in the TOC and fragment the document structure.
- **Do NOT bury navigable content under `###`** when it deserves its own TOC entry. For example:
  - ❌ Bad: `## DRY` → `### Bad Code Example` → `### Good Code Example`
  - ✅ Good: `## DRY — Overview`, `## DRY — Bad Code Example`, `## DRY — Good Code Example`
- Use `---` dividers between every `##` section for clean visual pacing.
- Use **bolding** for critical technical terms, class names, and keywords.
- Use inline backticks for code identifiers, types, methods, and parameters (e.g., `login()`, `String`, `User`).

### Heading Naming Patterns

The repo uses two established `##`/`###` patterns depending on how deeply a concept needs to be broken down. Choose the right one based on content complexity.

---

**Pattern A — Flat `##` sections** *(use when each sub-topic is independently navigable)*

Each sub-topic gets its own `##` heading. If a single concept spans multiple sections (overview, code example, caveat, comparison), prefix each `##` with the concept name to keep the TOC self-describing:

```
## <Concept>                          ← definition + diagram
## <Concept> — Code Example           ← code walkthrough
## <Concept> — Applying in Practice   ← how-to guidelines
## <Concept> — When NOT to Apply      ← caveats and exceptions
```

Real examples from this repo (`09.polymorphism.md`, `10.abstraction.md`, `02.software-design-principles.md`):
```
## 1. Compile-Time Polymorphism (Static Polymorphism)
## 2. Run-Time Polymorphism (Dynamic Polymorphism)
## Compile-Time vs Run-Time Polymorphism

## 1. Abstract Classes
## 2. Interface
## Abstract Class vs Interface
```

---

**Pattern B — `##` parent + `###` children** *(use when sub-items are tightly grouped and not independently navigable)*

A `##` section introduces a concept; `###` headings name tightly-related sub-items (e.g., numbered variants, labeled examples, named keypoints). This pattern is correct when the sub-items only make sense as part of the parent and don't need their own TOC slot:

```
## <Parent Concept>
### 1. <Variant or Sub-Type>
### 2. <Variant or Sub-Type>
### 3. <Variant or Sub-Type>
```

Real examples from this repo (`13.inner-classes.md`, `08.inheritance.md`, `12.static-keyword.md`, `19.solid-principles.md`):
```
## Types of Inner Classes
### 1. Static Nested Classes
### 2. Non-Static Inner Classes
### 3. Local Inner Classes

## 1. Single Responsibility Principle (SRP)
### Definition
### Explanation
### Example

## Static Variables in Java
### Definition
### When to Use
### Example
```

---

**Decision Rule — Which pattern to use?**

| Situation | Pattern |
| :--- | :--- |
| Sub-topic has its own code block, diagram, or needs direct TOC access | **Pattern A** — promote to `##` |
| Sub-topic is a numbered variant, named sub-type, or tightly-grouped label | **Pattern B** — use `###` under a `##` parent |
| Content is a brief inline clarification (a sentence or two) | Use **bold text** in the body, not a heading at all |

**Never use `####` (H4)** — it is invisible in the TOC and should be replaced with either a `###`, a bold label, or restructured as a separate `##` section.

### Code Snippets
- **Primary Language:** All code examples must be in **Java** unless the user explicitly requests another language.
- **Completeness:** Write clean, complete, idiomatic Java code with class declarations, proper access modifiers (`private`, `public`, `protected`), constructors, and a runnable `main()` method when demonstrating client usage.
- **Imports:** Include standard library imports (`import java.util.*;`) where relevant.
- **Comments:** Include concise inline comments explaining non-trivial logic.

### Visual Diagrams (Mermaid)
Always include at least one relevant Mermaid diagram when explaining relationships, architectures, or workflows:
- **Class Relationships & OOP:** Use `mermaid classDiagram` (showing inheritance `<|--`, composition `*--`, aggregation `o--`, or implementation `<|..`).
- **Architectural / Flowcharts:** Use `mermaid flowchart LR` or `graph TD` for component interactions and step-by-step logic.
- **Lifecycles & Interactions:** Use `mermaid sequenceDiagram` or `stateDiagram-v2` for object lifecycles and messaging.

### Comparison Tables
- Use clean Markdown tables with header alignment markers (`| :--- | :--- | :--- |`).
- Compare concepts across clear dimensions: Purpose, Level of Detail, Focus, Implementation, Advantages, and Trade-offs.

---

## 4. Content Completeness & Fidelity Rules

> [!IMPORTANT]
> **Zero Information Loss Principle:** Never omit, skip, or over-summarize any information, concept, example, analogy, link, or note provided by the user.

- **Complete Inclusion:** Every piece of information, note, prerequisite, stakeholder mention, distinction, or nuance present in the user's raw input must be faithfully preserved and represented in the final note.
- **Additive Expansion (No Degradation):**
  - **DO:** Add more content, richer context, full runnable Java implementations, detailed architectural explanations, edge cases, and Mermaid diagrams to elevate the quality of the note.
  - **DO NOT:** Strip away, overly condense, or alter the meaning of user-provided points.
- **Preserve User Examples & Domain Models:** If the user supplies specific domain examples (e.g., house construction, `AuthService`, `EmailNotification`, `login()`, `forgotPassword()`), preserve those exact names, relationships, and concepts in the code and explanations.

---

## 5. Processing Workflow: Raw Text to Standard Note

When the user provides raw text, notes, or interview transcript:

1. **Inspect Workspace Context:**
   - Check the target directory using `list_dir` to determine the latest file index number (e.g. `02`, `03`).
2. **Audit Raw Input for 100% Coverage:**
   - List all concepts, examples, analogies, notes, and links from the user's input to guarantee zero omission.
3. **Structure & Enrich:**
   - Extract the core topic and formulate an informative title and tagline blockquote.
   - Organize all provided points into the standard hierarchy (`What You'll Learn`, definitions, code examples, comparisons, and summary).
   - Expand terse or incomplete code snippets into fully formed, clean Java classes.
   - Add at least one relevant Mermaid diagram mapping out the concept.
4. **Apply TOC Compatibility:**
   - Before writing, plan out the full heading hierarchy on paper.
   - Every sub-topic, code example, caveat, and benefit that is a distinct navigable item MUST be a `##` heading — not `###` or `####`.
   - Use the prefixed naming pattern: `## ConceptName — SubtopicName` for multi-part concepts.
5. **Write & Validate:**
   - Use `write_to_file` to create `XX.<topic-name>.md` in the designated directory.
   - Verify the generated markdown for complete coverage, syntax correctness, valid mermaid syntax, and clean layout.
   - **TOC check:** Mentally scan the heading list — every major item should be at `##` level and clickable in the IDE TOC panel.
