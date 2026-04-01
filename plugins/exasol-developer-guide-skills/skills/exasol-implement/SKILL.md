---
name: exasol-developer-guide:implement
version: 2.0.0
description: |
  Write RST files to disk based on a plan from /exasol-developer-guide:new or /exasol-developer-guide:modify.
  Clones the GitHub repo fresh, implements changes, sets up a Python virtual environment,
  runs poetry install and the Sphinx build to verify, fixes any errors, then pushes to
  a new branch on GitHub. Asks the user for the branch name before starting.
allowed-tools:
  - Read
  - Glob
  - Grep
  - Write
  - Edit
  - Bash
  - AskUserQuestion
---

## Step 0 — Check for Plan

Look for a plan in the current conversation from `/exasol-developer-guide:new` or `/exasol-developer-guide:modify`.
If no plan is present, respond:
> "No plan found. Please run `/exasol-developer-guide:new` or `/exasol-developer-guide:modify` first."

---

## Step 1 — Ask for Branch Name

Ask the user:
> "What should the Git branch name be for these changes?"

Wait for the response before continuing.

---

## Step 2 — Locate the Repository

Ask the user:
> "Do you have a local folder for the developer-documentation repo? If yes, provide the path. If not, just say no and I will clone it."

**If the user provides a folder path:**
- Use that folder as the working directory for all subsequent steps
- Run `git pull` inside it to ensure it is on the latest version:

```bash
cd <provided-folder>
git pull
```

**If the user does not provide a folder:**
- Clone the repo into the current working directory:

```bash
git clone https://github.com/exasol/developer-documentation.git
```

- Use the newly cloned directory for all subsequent steps.

All file operations (reads and writes) happen inside the resolved directory — do not use any hardcoded absolute paths.

---

## Step 3 — Implement Each File

Write or edit each RST file in the cloned directory according to the plan. Follow all RST conventions below strictly.

### RST Formatting Rules

#### Heading Levels

```
Document Title (H1) — overline AND underline with =, both must be >= title length
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

**Critical:** Count the exact character length of the title text. The overline and underline must be at least that many characters. Off-by-one causes a build error.

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

---

## Step 5 — Update Toctrees

**New section folder created:**
1. Read `doc/index.rst` in the cloned directory
2. Add the new entry to the toctree at the position specified in the plan
3. Write the updated `doc/index.rst`

**New file added to an existing section:**
1. Read the section's `index.rst`
2. Add the new filename (without `.rst`) to the toctree in logical order
3. Write the updated `index.rst`

---

## Step 6 — Set Up Environment and Test the Build

From inside the cloned directory, run:

```bash
# Create virtual environment
python -m venv .venv

# Activate it (Windows bash / Git Bash)
source .venv/Scripts/activate

# Install project dependencies via Poetry
poetry install

# Run the Sphinx docs build
poetry run nox -s docs:build
```

**If the build reports warnings treated as errors:**
- Read the error output carefully to identify the file and line number
- Fix the RST issue in the relevant file (common causes: overline too short, bad indentation, missing blank line before directive)
- Re-run `poetry run nox -s docs:build`
- Repeat until the build reports: `build succeeded`

---

## Step 7 — Commit and Push

Once the build succeeds:

```bash
git checkout -b <branch-name>
git add doc/
git commit -m "Add documentation: <short description from plan>"
git push -u origin <branch-name>
```

---

## Step 8 — Report

Output a final summary:

```
Repository cloned from: https://github.com/exasol/developer-documentation.git
Branch pushed:          <branch-name>

Files created:
  doc/[section]/index.rst
  doc/[section]/overview.rst
  ...

Files modified:
  doc/index.rst  (added toctree entry: [section]/index)
  ...

Build: PASSED

Create PR at: https://github.com/<org>/<repo>/pull/new/<branch-name>
```

If anything from the plan could not be fully implemented, note it so the user can follow up.
