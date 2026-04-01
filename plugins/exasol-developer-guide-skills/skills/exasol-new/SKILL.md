---
name: exasol-developer-guide:new
version: 2.0.0
description: |
  Plan a new developer guide section for an Exasol feature, connector, or tool.
  Searches docs.exasol.com, github.com/exasol, and PyPI for content, asks clarifying
  questions, then produces a structured plan ready for /exasol-developer-guide:implement.
  Usage: /exasol-developer-guide:new [feature or topic name]
allowed-tools:
  - Read
  - Glob
  - Grep
  - Bash
  - WebSearch
  - WebFetch
  - AskUserQuestion
---

## Context

- **Project root:** Detect by running `git rev-parse --show-toplevel` — do not use hardcoded paths
- **Docs root:** `<project-root>/doc/`
- **File format:** reStructuredText (`.rst`) rendered by Sphinx
- **Target audience:** Data professionals and developers — professional but accessible
- **Gold standard:** `doc/connect_to_exasol/` (connectors) and `doc/gen_ai/ai_text_summary/` (tutorials)
- **Standard structure:** What → How (step-by-step with code) → Benefits + Real-world use cases + Examples

## Step 1 — Identify the Subject

If the user provided a feature/topic name as an argument, use it. If not, ask:
> "What feature, connector, or tool do you want to document?"

## Step 2 — Research Online

Use WebSearch and WebFetch to gather information from all of the following:

- Search: `site:docs.exasol.com [topic]` — official Exasol documentation
- Search: `site:github.com/exasol [topic]` — Exasol GitHub repositories
- Search: `site:pypi.org [topic] exasol` — Python packages (if applicable)
- Search: `[topic] exasol tutorial getting started`
- Search: `[topic] exasol example`

Fetch the most relevant pages found. Extract:
- What the feature/tool does and why it exists
- Key concepts and terminology
- Official API / configuration parameters
- Code examples and usage patterns
- Prerequisites and system requirements
- Common real-world use cases
- Links to authoritative external documentation

## Step 3 — Read the Existing Project

Detect the project root:
```bash
git rev-parse --show-toplevel
```

Then read the following (relative to that root) to ensure the new section fits project conventions:
- `doc/index.rst` — current top-level toctree structure
- `doc/connect_to_exasol/index.rst` and one content file from it
- `doc/gen_ai/ai_text_summary/index.rst`

## Step 4 — Ask Clarifying Questions

Before sketching the plan, ask:

1. Is this a **connector**, a **feature**, a **tool**, or a **tutorial/example**?
2. Who is the primary user — data engineers, analysts, data scientists, or all?
3. Are there existing code examples or GitHub repos to reference?
4. Any specific aspects to emphasize — performance, ease of setup, integrations?
5. Should this be a **top-level section** in `doc/` or a **subsection** of an existing one?
6. Any topics to exclude or keep minimal?

Wait for responses before sketching the plan.

## Step 5 — Sketch the Plan

### Proposed Folder Structure

```
doc/[section-folder-name]/
├── index.rst          — Section landing page with toctree
├── overview.rst       — What: definition, key concepts, system requirements
├── installation.rst   — (if applicable) setup, dependencies, pip commands
├── [descriptive].rst  — How: step-by-step with working code examples
└── [examples].rst     — Real-world use cases and complete end-to-end examples
```

Adjust files based on complexity and content type.

### Per-File Content Plan

For each file state:
- **Title**
- **Sections/headings** to include
- **Key content points** (bullet list — not full RST)
- **Code examples** to include (language + what the example shows)
- **External links** to reference (from Step 2 research — real URLs only)

### Toctree Update

State exactly:
- Which position in `doc/index.rst` to insert the new entry
- The exact toctree entry string (e.g., `   [folder]/index`)

### Cross-References

Note any `:ref:` links to/from existing sections that should be added.

**Do NOT write any files. This skill produces a plan only.**
**The user will run `/exasol-developer-guide:implement` to write the files once the plan is approved.**
