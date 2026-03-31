# Exasol Developer Guide Creator

> AI-powered Claude Code skills for building and maintaining professional Exasol documentation — research, plan, and write RST content without leaving your editor.

---

## What it does

Writing great technical documentation is slow. You switch between the Exasol docs, GitHub, PyPI, your editor, and a blank page — then spend hours figuring out the right structure. This plugin gives Claude Code four focused skills that handle the research, structure, and writing for you.

The result: consistent, professional reStructuredText sections that follow the **What → How → Benefits** standard used throughout the Exasol developer guide.

---

## The four skills

```
/exasol-developer-guide:explore           # audit the whole project
/exasol-developer-guide:new <topic>       # plan a new section
/exasol-developer-guide:modify <section>  # plan changes to an existing section
/exasol-developer-guide:implement         # write the files
```

| Skill | What it does |
|---|---|
| **:explore** | Reads your entire `doc/` tree, rates each section against the content standard, and produces a prioritised improvement plan via interactive Q&A |
| **:new `<topic>`** | Searches `docs.exasol.com`, `github.com/exasol`, and PyPI for your topic, asks clarifying questions, then outputs a complete file-and-folder plan |
| **:modify `<section>`** | Reads the existing section, optionally checks for upstream changes online, Q&As with you to agree scope, and outputs a per-file change list |
| **:implement** | Takes the plan from `:new` or `:modify` and writes the actual `.rst` files — headings, code blocks, toctrees, cross-references, all formatted correctly |

> **Planning is always separate from writing.** You review and approve the plan before a single file is touched.

---

## Typical workflows

**Document a new feature**
```
/exasol-developer-guide:new kafka connector
```
Claude researches the connector, asks what to include, proposes a folder structure. When you're happy:
```
/exasol-developer-guide:implement
```

**Improve an existing section**
```
/exasol-developer-guide:modify UDF
```
Claude reads the current files, identifies gaps (missing prerequisites, no code examples, outdated API), agrees a change list with you, then:
```
/exasol-developer-guide:implement
```

**Full project audit**
```
/exasol-developer-guide:explore
```
Get a scored overview of every section with specific improvement suggestions ranked by impact. Then run `:new` or `:modify` on the sections you want to fix.

---

## Installation

### Recommended: Claude Marketplace

This is the easiest way — no Git or file management required. Just open Claude Code and run two commands, one after the other.

**Step 1 — Add the plugin to your marketplace:**
```
/plugin marketplace add exasol-labs/exasol-developer-guide-skills
```

**Step 2 — Install it into Claude Code:**
```
/plugin install exasol-developer-guide-skills@exasol-developer-guide-skills
```

That's it. The skill is now available. Type `/skills` to confirm it's listed.

---

### Alternative: Manual installation

Use this method if you prefer to manage files yourself or don't have marketplace access.

**Step 1 — Clone the repository:**
```bash
git clone https://github.com/exasol-labs/exasol-developer-guide-skills.git
```

**Step 2 — Copy it into Claude Code's skills folder:**
```bash
cp -r exasol-developer-guide-skills ~/.claude/skills/exasol-developer-guide
```

**Step 3 — Restart Claude Code.**

The skill will appear in your `/skills` list as `exasol-developer-guide`.

---

## Project structure expected

The skills are designed for a Sphinx-based documentation project:

```
your-project/
└── doc/
    ├── index.rst          ← top-level toctree
    ├── connect_to_exasol/ ← connector section
    ├── gen_ai/            ← tutorial section
    └── ...
```

- **Format:** reStructuredText (`.rst`) rendered by Sphinx
- **Audience:** Data professionals and developers
- **Content standard:** What → How (with working code examples) → Benefits + real-world use cases

---

## Adapting to a different project

To point these skills at a different documentation project, update the `**Project path:**` line in each `SKILL.md` file inside the sub-skill folders.

---

## Author

Muhammad Abdullah Farooqui · [abdullahfarooqui094@gmail.com](mailto:abdullahfarooqui094@gmail.com)
