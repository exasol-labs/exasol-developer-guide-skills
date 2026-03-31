---
name: exasol-developer-guide:implement
version: 1.0.0
description: |
  Write RST files to disk based on a plan from /exasol-developer-guide:new or /exasol-developer-guide:modify.
  Confirms before writing, creates all files and folders, updates parent toctrees,
  and reports everything created or modified. Requires a plan in the conversation.
allowed-tools:
  - Read
  - Glob
  - Grep
  - Write
  - Edit
  - Bash
---

## Prerequisites

A plan **must already exist** in this conversation from `/exasol-developer-guide:new` or `/exasol-developer-guide:modify`.
If no plan is present, respond: "No plan found. Please run `/exasol-developer-guide:new` or `/exasol-developer-guide:modify` first."

## Context

- **Project path:** `C:\Users\mufa\documents\developer-documentation`
- **Docs root:** `doc/`
- **File format:** reStructuredText (`.rst`) rendered by Sphinx
- **Target audience:** Data professionals and developers — professional but accessible
- **Standard structure:** What → How (step-by-step with code) → Benefits + Real-world use cases + Examples

---

## Step 1 — Confirm

Summarise what will be written or modified from the plan:
- Files to be created (with paths)
- Files to be modified (with paths)
- Toctree entries to be added

Ask: "Ready to implement — shall I proceed?"

Wait for confirmation before writing anything.

---

## Step 2 — Implement Each File

Write or edit each file according to the plan. Strictly follow the RST conventions below.

### RST Formatting Rules

#### Heading Levels

```
Document Title (H1) — overline AND underline with =
===================
Document Title
===================

Section Heading (H2) — underline only with =
Section Title
=============

Subsection (H3) — underline with -
Subsection Title
----------------

Sub-subsection (H4) — underline with ^
Sub-subsection
^^^^^^^^^^^^^^
```

The overline/underline must be at least as long as the text.

#### Code Blocks

```rst
.. code-block:: python

    import pyexasol
    connection = pyexasol.connect(dsn='host:port', user='sys', password='exasol')
```

Always specify language: `python`, `sql`, `bash`, `text`, `json`.
Indent code content by 4 spaces inside the directive.

#### Notes and Warnings

```rst
.. note::
   Text here, indented 3 spaces.

.. warning::
   Text here.

.. important::
   Text here.
```

#### Tables

```rst
.. list-table:: Optional Title
   :header-rows: 1
   :widths: 25 75

   * - Column One
     - Column Two
   * - Row value
     - Row value
```

#### Links

```rst
`Link text <https://url>`_
```

#### Internal Cross-References

```rst
.. _my-label:

Section Title
=============

(to reference it elsewhere)
:ref:`my-label`
```

#### Toctree

```rst
.. toctree::
   :maxdepth: 2

   overview
   installation
   usage
   subdir/index
```

Do NOT include `.rst` extension in toctree entries.

#### Inline Formatting

```rst
**bold**   *italic*   ``inline code``
```

### Content Standards

- **Tone:** Professional but accessible — not overwhelming, not condescending
- **Every "How" section** must have at least one working, copy-paste ready code example
- **Prerequisites** must appear before any step-by-step instructions
- **Structure:** What → How → Benefits + Real-world examples throughout
- **Sections stay focused** — split into subsections if content exceeds ~60 lines
- **Cross-references:** Add `:ref:` links to related sections where relevant
- **External links:** Use real URLs from the plan research only — never invent URLs
- **Code examples:** Use realistic but simple values (e.g., schema `DEMO`, table `EMPLOYEES`)

---

## Step 3 — Update Toctrees

**New section folder created:**
1. Read `doc/index.rst`
2. Add the new entry to the toctree at the position specified in the plan
3. Write the updated `doc/index.rst`

**New file added to an existing section:**
1. Read the section's `index.rst`
2. Add the new filename (without `.rst`) to the toctree in logical order
3. Write the updated `index.rst`

---

## Step 4 — Report

After all files are written, output a summary:

```
Files created:
  doc/[section]/index.rst
  doc/[section]/overview.rst
  ...

Files modified:
  doc/index.rst  (added toctree entry: [section]/index)
  ...
```

If anything in the plan was unclear or could not be fully implemented, note it so the user can follow up.
