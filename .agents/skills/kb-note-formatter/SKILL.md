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

## <Concept 1: Definition & Real-World Analogy>

<Clear explanation of the concept, breaking down jargon into intuitive terms.>

### Real-Life Analogy
<Intuitive real-world analogy (e.g., house construction, banking system, car manufacturing).>

```mermaid
<Visual diagram illustrating the workflow, architecture, or object hierarchy>
```

---

## <Concept 2: Technical Deep Dive & Java Code Implementation>

<Detailed explanation of technical mechanisms, rules, and lifecycle.>

### Code Example

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

## Key Points & Best Practices

- **<Point 1>:** <Explanation>
- **<Point 2>:** <Explanation>
- **<Point 3>:** <Explanation>

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
- Use a single `#` for the main title at the top of the file.
- Use `##` for primary sections and `###` for sub-sections.
- Use `---` dividers between major sections for clean visual pacing.
- Use **bolding** for critical technical terms, class names, and keywords.
- Use inline backticks for code identifiers, types, methods, and parameters (e.g., `login()`, `String`, `User`).

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
4. **Write & Validate:**
   - Use `write_to_file` to create `XX.<topic-name>.md` in the designated directory.
   - Verify the generated markdown for complete coverage, syntax correctness, valid mermaid syntax, and clean layout.

