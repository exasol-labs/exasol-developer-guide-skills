---
name: exasol-developer-guide:explore
version: 2.0.0
description: |
  Audit the Exasol developer guide structure. Detects the project root from git,
  crawls all sections, rates quality against the What→How→Benefits standard, then does
  interactive Q&A with the user to co-create a prioritised improvement plan.
allowed-tools:
  - Read
  - Glob
  - Grep
  - Bash
  - AskUserQuestion
  - WebSearch
  - WebFetch
---

## Context

- **Project root:** Ask the user for their local repo path, or clone it — do not use hardcoded paths
- **Docs root:** `<repo-root>/doc/`
- **File format:** reStructuredText (`.rst`) rendered by Sphinx
- **Target audience:** Data professionals and developers — professional but accessible
- **Gold standard sections:** `doc/connect_to_exasol/` and `doc/gen_ai/ai_text_summary/`

## Step 1 — Locate the Repository

Ask the user:
> "Do you have a local folder for the developer-documentation repo? If yes, provide the path. If not, just say no and I will clone it."

**If the user provides a folder path:**
- Use that folder as the working directory for all subsequent steps.
- Run `git pull` inside it to ensure it is up to date:

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

All file operations happen inside the resolved directory — do not use any hardcoded absolute paths.

## Step 2 — Explore

Read the following in parallel using Glob and Read tools (relative to the resolved repo root):
- Full folder/file tree of `doc/` (Glob pattern: `doc/**/*`)
- `doc/index.rst` — top-level toctree
- Every `index.rst` inside section subfolders
- 2–3 representative content files per section (the most substantial ones)

Do NOT skip any section folder. Read actual file contents, not just filenames.

## Step 3 — Assess Each Section

Evaluate every section against the developer guide standard:

**Expected structure per section:**
1. **What** — Clear definition: what the feature/tool is, why it exists
2. **How** — Step-by-step implementation with working, copy-paste-ready code examples
3. **Benefits + Real-world use cases** — Practical scenarios, when to use it, what it enables

**Quality checklist per section:**
- Tone: professional but accessible — not overwhelming, not condescending
- Prerequisites clearly stated before any steps
- Code examples present and complete (not just snippets)
- Information up to date (no outdated version references)
- Cross-references to related sections present where relevant
- Follows What → How → Benefits structure

## Step 4 — Interactive Q&A

Present findings in this structure:

1. **Current state** — Table of all sections with a brief quality rating: Good / Needs Work / Incomplete / Missing
2. **Gaps identified** — Features or tools that exist in the Exasol ecosystem but have no section yet
3. **Specific improvement areas** — Be concrete: e.g., "UDF/debugging.rst is only one sentence, needs a real debugging walkthrough"
4. **Ranked suggestions** — List improvements ordered by impact (High / Medium / Low)

Then ask targeted questions:
- Which improvements matter most right now?
- Any specific features or connectors to document next?
- Sections to fully restructure vs. just expand?
- Anything to remove or consolidate?

Wait for user responses before proceeding.

## Step 5 — Sketch the Plan

Based on Q&A responses, produce a concrete action plan. For each proposed change state:
- Section name and file(s) affected
- Type of change: **new section** / **add content** / **restructure** / **simplify**
- Brief description of what will change and why
- Priority: High / Medium / Low

Note which changes need `/exasol-developer-guide:new` (new sections), `/exasol-developer-guide:modify` (restructuring), or can go straight to `/exasol-developer-guide:implement` (simple additions).

**Do NOT write any files. This skill is exploration and planning only.**
