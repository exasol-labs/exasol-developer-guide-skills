---
name: exasol-developer-guide
version: 1.0.0
description: |
  Create and maintain the Exasol developer guide — a simplified, marketable
  documentation site for Exasol features, connectors, and tools. Four workflows:
  explore (audit & plan), new (plan a new section), modify (plan changes to an
  existing section), implement (write RST files to disk).
  Usage: /exasol-developer-guide (shows this help menu)
allowed-tools:
  - Read
  - Glob
  - Grep
  - Write
  - Edit
  - Bash
  - WebSearch
  - WebFetch
  - AskUserQuestion
---

## Help display

Print the following usage menu and stop. Do not run any workflow.

```
Exasol Developer Guide

  /exasol-developer-guide:explore              Audit the doc structure and co-create an improvement plan
  /exasol-developer-guide:new <topic>          Plan a new section (e.g. /exasol-developer-guide:new kafka connector)
  /exasol-developer-guide:modify <section>     Plan changes to an existing section (e.g. /exasol-developer-guide:modify UDF)
  /exasol-developer-guide:implement            Write RST files to disk based on the current plan
```

---

## Context (applies to all workflows)

- **Project path:** `C:\Users\mufa\documents\developer-documentation`
- **Docs root:** `doc/`
- **File format:** reStructuredText (`.rst`) rendered by Sphinx
- **Target audience:** Data professionals and developers — professional but accessible
- **Standard content structure:** What → How (step-by-step with code) → Benefits + Real-world use cases + Examples
- **Gold standard sections:** `doc/connect_to_exasol/` and `doc/gen_ai/ai_text_summary/`
- **Online sources:** `docs.exasol.com`, `github.com/exasol`, `pypi.org`

---

## Workflow: explore

Audit the existing developer guide, surface improvement opportunities, and co-create an action plan through interactive Q&A.

### Step 1 — Explore the Project

Read in parallel using Glob and Read:
- Full file tree of `doc/` (Glob: `doc/**/*`)
- `doc/index.rst`
- Every `index.rst` inside section subfolders
- 2–3 representative content files per section (the most substantial ones)

### Step 2 — Assess Each Section

Evaluate every section against the standard:

1. **What** — Clear definition: what the feature/tool is, why it exists
2. **How** — Step-by-step implementation with working, copy-paste-ready code examples
3. **Benefits + Real-world use cases** — Practical scenarios

Quality checklist:
- Tone: professional but accessible — not overwhelming, not condescending
- Prerequisites stated before steps
- Code examples complete and runnable
- Information up to date
- Cross-references to related sections present
- Follows What → How → Benefits structure

### Step 3 — Interactive Q&A

Present findings:
1. **Current state** — Table of all sections rated: Good / Needs Work / Incomplete / Missing
2. **Gaps** — Features in the Exasol ecosystem with no section yet
3. **Specific issues** — Concrete problems per file (e.g., "UDF/debugging.rst is one sentence — needs a real walkthrough")
4. **Ranked suggestions** — High / Medium / Low impact

Then ask:
- Which improvements matter most right now?
- Specific features or connectors to document next?
- Sections to restructure vs. just expand?
- Anything to remove or consolidate?

Wait for responses.

### Step 4 — Sketch the Plan

For each proposed change state: section, files affected, type (new / add content / restructure / simplify), description, priority.
Note which changes need `new`, `modify`, or can go straight to `implement`.

**Do NOT write any files.**

---

## Workflow: new

Plan a brand-new documentation section for an Exasol feature, connector, or tool.

### Step 1 — Identify the Subject

Use the topic from the user's arguments. If not provided, ask: "What feature, connector, or tool do you want to document?"

### Step 2 — Research Online

Search using WebSearch and WebFetch:
- `site:docs.exasol.com [topic]`
- `site:github.com/exasol [topic]`
- `site:pypi.org [topic] exasol`
- `[topic] exasol tutorial getting started`

Extract: what it does, key concepts, API parameters, code examples, prerequisites, use cases, authoritative links.

### Step 3 — Read the Existing Project

Read for consistency:
- `doc/index.rst`
- `doc/connect_to_exasol/index.rst` and one content file
- `doc/gen_ai/ai_text_summary/index.rst`

### Step 4 — Ask Clarifying Questions

1. Is this a connector, feature, tool, or tutorial/example?
2. Primary user — data engineers, analysts, data scientists, or all?
3. Existing code examples or GitHub repos to reference?
4. Specific aspects to emphasise — performance, ease of setup, integrations?
5. Top-level section in `doc/` or subsection of an existing one?
6. Topics to exclude or keep minimal?

Wait for responses.

### Step 5 — Sketch the Plan

**Proposed folder structure:**
```
doc/[section-folder]/
├── index.rst          — landing page + toctree
├── overview.rst       — What: definition, concepts, system requirements
├── installation.rst   — (if applicable) setup, dependencies
├── [usage].rst        — How: step-by-step with working code examples
└── [examples].rst     — Real-world use cases and end-to-end examples
```

For each file: title, headings, key content points, code examples (language + what it shows), external links (real URLs from research only).

Toctree update: exact position in `doc/index.rst` and the entry string.

Cross-references: any `:ref:` links to/from existing sections.

**Do NOT write any files.**

---

## Workflow: modify

Plan changes to an existing developer guide section.

### Step 1 — Locate the Section

Use the section name from the user's arguments. If not provided, ask: "Which section do you want to modify?"

Use Glob to list all files in the section folder, then Read every file.

### Step 2 — Assess the Current Content

Check each file for:
- Missing What / How / Benefits structure
- Incomplete or non-runnable code examples
- Outdated information (old versions, deprecated APIs, broken links)
- Tone issues — too technical, too vague, condescending
- Missing prerequisites
- Missing cross-references
- Content too dense (needs splitting) or too thin (needs expanding)

### Step 3 — Research Online (if relevant)

If the section covers a specific tool or API:
- `site:docs.exasol.com [topic]`
- `site:github.com/exasol [topic]`

Check for new versions, changed APIs, new features, deprecated functionality.

### Step 4 — Interactive Q&A

Present:
1. What exists — summary per file
2. What's missing — gaps against the standard
3. What needs fixing — specific issues
4. What could be cut — redundant or outdated content

Then ask:
1. What prompted this request?
2. New features, API changes, or corrections to document?
3. File structure to keep or change?
4. New code examples to add?
5. Anything to remove or simplify?

Wait for responses.

### Step 5 — Sketch the Modification Plan

For each file: path, current state (one line), specific changes (precise — not vague), new content to add, content to remove, structural changes.

**Do NOT write any files.**

---

## Workflow: implement

Write RST files to disk based on a plan from `new` or `modify`.

### Step 0 — Check for Plan

Look for a plan in the current conversation. If none exists, respond: "No plan found. Please run `explore`, `new`, or `modify` first."

### Step 1 — Confirm

List all files to be created and modified. Ask: "Ready to implement — shall I proceed?" Wait for confirmation.

### Step 2 — Write the Files

Follow these RST conventions strictly:

**Headings:**
```rst
===================
Document Title (H1)    ← overline + underline with =
===================

Section (H2)
============

Subsection (H3)
---------------

Sub-subsection (H4)
^^^^^^^^^^^^^^^^^^^
```
Overline/underline must be at least as long as the text.

**Code blocks:**
```rst
.. code-block:: python

    code here (4-space indent)
```
Languages: `python`, `sql`, `bash`, `text`, `json`

**Admonitions:**
```rst
.. note::
   Text (3-space indent)

.. warning::
   Text

.. important::
   Text
```

**Tables:**
```rst
.. list-table:: Title
   :header-rows: 1
   :widths: 25 75

   * - Col 1
     - Col 2
   * - Value
     - Value
```

**Links:** `` `text <https://url>`_ ``

**Cross-references:**
```rst
.. _label-name:

Title
=====

:ref:`label-name`
```

**Toctree** (no `.rst` extension in entries):
```rst
.. toctree::
   :maxdepth: 2

   overview
   installation
   usage
```

**Inline:** ``**bold**``, ``*italic*``, ` `` inline code `` `

**Content standards:**
- Professional but accessible — not overwhelming, not condescending
- Every "How" section: at least one working, copy-paste-ready code example
- Prerequisites before any step-by-step instructions
- What → How → Benefits structure throughout
- Split into subsections if a file exceeds ~60 lines
- Add `:ref:` links to related sections where relevant
- External links: real URLs from the plan only — never invent URLs

### Step 3 — Update Toctrees

New section folder: read `doc/index.rst`, add entry at the position from the plan, write it.

New file in existing section: read the section's `index.rst`, add filename (no `.rst`) in logical order, write it.

### Step 4 — Report

```
Files created:
  doc/[section]/index.rst
  ...

Files modified:
  doc/index.rst  (toctree: added [section]/index)
  ...
```

Note anything from the plan that could not be fully implemented.
