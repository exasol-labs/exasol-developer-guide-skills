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

- **Project root:** Detect by running `git rev-parse --show-toplevel` — do not use hardcoded paths
- **Docs root:** `<project-root>/doc/`
- **File format:** reStructuredText (`.rst`) rendered by Sphinx
- **Target audience:** Data professionals and developers — professional but accessible
- **Gold standard sections:** `doc/connect_to_exasol/` and `doc/gen_ai/ai_text_summary/`

## Step 1 — Detect Project Root and Explore

First detect the project root:
```bash
git rev-parse --show-toplevel
```

Then read the following in parallel using Glob and Read tools (relative to that root):
- Full folder/file tree of `doc/` (Glob pattern: `doc/**/*`)
- `doc/index.rst` — top-level toctree
- Every `index.rst` inside section subfolders
- 2–3 representative content files per section (the most substantial ones)

Do NOT skip any section folder. Read actual file contents, not just filenames.

## Step 2 — Assess Each Section

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

## Step 3 — Interactive Q&A

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

## Step 4 — Sketch the Plan

Based on Q&A responses, produce a concrete action plan. For each proposed change state:
- Section name and file(s) affected
- Type of change: **new section** / **add content** / **restructure** / **simplify**
- Brief description of what will change and why
- Priority: High / Medium / Low

Note which changes need `/exasol-developer-guide:new` (new sections), `/exasol-developer-guide:modify` (restructuring), or can go straight to `/exasol-developer-guide:implement` (simple additions).

**Do NOT write any files. This skill is exploration and planning only.**
