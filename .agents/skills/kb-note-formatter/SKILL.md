---
name: kb-note-formatter
description: >-
  Use this skill when the user pastes plain/raw text content (notes, dumps,
  copied articles, rough drafts) and wants it turned into a properly formatted
  Markdown file for this knowledge base. Activate when the user says things
  like "format this", "make this an md file", "convert this to a note",
  "add this to the knowledge base", or pastes a wall of unformatted text.
  This skill derives the correct file name, folder, and all structural
  formatting rules from the established conventions in this repository.
---

# Knowledge Base Note Formatter

This skill converts raw/plain text into a properly structured Markdown note
that matches the formatting conventions used across this knowledge base
(`d:\knowledge-base`).

---

## Step 1 - Understand the Repository Conventions

Before formatting, confirm you understand the following rules by cross-checking
with the existing files. These rules were derived from analysing all files in
the `Object Oriented Programming/`, `Low Level Design/`, and `JAVA/` folders.

### File Naming Convention

The pattern is: `NN.kebab-case-topic-name.md`

- `NN` = zero-padded two-digit sequence number that continues from the **last
  existing file** in the target folder (e.g. if last file is `06.encapsulation.md`,
  the new file is `07.new-topic.md`).
- The slug after the number is the topic in **lowercase kebab-case** - no
  abbreviations, no underscores.
- Determine the correct **target folder** from the topic (OOP concept ->
  `Object Oriented Programming/`, LLD concept -> `Low Level Design/`,
  Java syntax -> `JAVA/`). Ask the user if ambiguous.

### Document Structure (top to bottom)

Every file must follow this structure in order:

1. `# Topic Title in Title Case`
2. `> One-line blockquote summarising the topic` (optional but strongly preferred)
3. `## What You'll Learn` section with a bullet list
4. `---` horizontal rule
5. Main content sections using `##` and `###`
6. `---` between every `##` section
7. `## Summary` table at the end

### Heading Hierarchy Rules (CRITICAL)

| Level | Use for |
| :--- | :--- |
| `#` | Document title - exactly one per file |
| `##` | Top-level sections (What You'll Learn, main topic sections, Summary) |
| `###` | Sub-sections that belong under a `##` parent |
| `####` | Rarely used; only for deeply nested sub-sub-sections |

IMPORTANT: Never use `##` for a section that logically belongs under another
`##` section. For example, "DRY - Bad Code Example" must be `###` because it
lives under `## 1. DRY`. Flat `##` hierarchies break the Table of Contents (TOC).

### Mandatory Sections

1. `# Title` - Required. Title Case.
2. `> blockquote` - Strongly preferred one-liner summary.
3. `## What You'll Learn` - Required. Bullet list of learning outcomes.
4. `---` separators - Required between every top-level `##` section.
5. `## Summary` - Required at the end. Always a markdown table.

### Optional but Common Sections

- `## Key Concept` or `## Key Characteristics` - for definitional content.
- `### [Topic] - Bad Code Example` and `### [Topic] - Good Code Example` as
  sub-sections under their parent `##` section.
- `## Importance of [Topic]` with `### Benefit 1: ...` sub-sections.
- GitHub alerts: `> [!NOTE]`, `> [!TIP]`, `> [!IMPORTANT]`, `> [!WARNING]`,
  `> [!CAUTION]` - use sparingly, never consecutive or nested.

### Code Blocks

- Always specify a language tag: java, mermaid, text, etc.
- Java code must include `import java.util.*;` when collections are used.
- Class and method names follow Java conventions (PascalCase / camelCase).

### Mermaid Diagrams

- Use `flowchart TD` or `flowchart LR` for process and concept flows.
- Use `classDiagram` for class/interface relationships.
- Quote node labels containing special characters: `["Label (Info)"]`.

### Tables

- Use aligned column separators: `| :--- | :--- |` (left-aligned for all columns).
- Bold the left-column concept/term: `| **Term** | Description |`.

### Content Fidelity Rule (CRITICAL)

**Preserve ALL content from the raw text exactly as pasted.** Do not:
- Add explanations, examples, or context that were not in the original text.
- Invent code examples only if none were provided.
- Summarise or shorten the user's content.
- Add filler sentences like "In this section we will..."

Your job is purely **structural reformatting** — apply headings, separators,
code blocks, and tables to what the user gave you. Every sentence from the
original must appear in the output.

The only exceptions allowed are:
- The `> blockquote` one-liner (derive it from the first sentence of the text).
- The `## What You'll Learn` bullets (derive them from the actual topics covered
  in the text, not invented topics).
- The `## Summary` table rows (summarise concepts that already appear in the text).

---

## Step 2 - Determine Target Folder and File Name

1. Identify the topic from the plain text.
2. Identify the correct folder:
   - OOP concepts (classes, objects, encapsulation, inheritance, etc.)
     -> `Object Oriented Programming/`
   - LLD concepts (design patterns, design principles, system components)
     -> `Low Level Design/`
   - Java language features (variables, data types, loops, arrays, etc.)
     -> `JAVA/`
   - Ask the user if the topic could belong to multiple folders.
3. Use `list_dir` to find the last file number in the target folder.
4. Construct the filename: `(last_number + 1).kebab-case-topic.md`

---

## Step 3 - Format the Content

Transform the raw text following all rules in Step 1.
Do NOT add content that was not in the original — only reformat/restructure:

1. Derive a one-line `>` blockquote summary from the opening of the text.
2. Derive `## What You'll Learn` bullets from the actual topics covered.
3. Identify logical sections in the text and assign correct `##` / `###` levels.
4. Wrap inline code references in backticks.
5. Wrap code snippets in fenced code blocks with the correct language tag.
6. Add `---` separators between every `##` section.
7. Write a `## Summary` table whose rows only reference concepts from the text.

Every sentence, paragraph, and code block from the raw text must appear
in the formatted output. Do not drop, shorten, or skip any of it.

---

## Step 4 - Create the File

Use `write_to_file` to create the file at:
  `d:\knowledge-base\<TargetFolder>\<NN.kebab-case-topic.md>`

After writing, confirm to the user:
- The full file path as a clickable link
- The heading structure (so they can verify the TOC will render correctly)
- Any assumptions made about folder or topic categorisation

---

## Reference Examples

Study these existing files to calibrate expected output quality:

- `Low Level Design/02.software-design-principles.md`
  Good example of `##` parent sections with `###` sub-sections.
  (DRY/KISS/YAGNI with Bad Code / Good Code examples nested under each.)

- `Object Oriented Programming/06.encapsulation.md`
  Good example of Key Concept, Example, Key Takeaways, Summary table,
  and a `> [!NOTE]` alert.

- `Object Oriented Programming/19.solid-principles.md`
  Good example of numbered main sections (`## 1. SRP`, `## 2. OCP`) each
  with `### Definition`, `### Explanation`, `### Example` sub-sections.

- `Object Oriented Programming/03.attribute-and-method.md`
  Good example of a simpler file: `> blockquote`, clean `##` sections,
  and `---` separators between every section.
