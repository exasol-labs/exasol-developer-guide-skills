# Exasol Developer Guide Creator Skills

A Claude Code skill bundle for creating and maintaining the Exasol developer guide — a simplified, marketable documentation site for Exasol features, connectors, and tools.

## Usage

All four workflows are available through a single command:

```
/exasol-developer-guide-creator explore
/exasol-developer-guide-creator new <topic>
/exasol-developer-guide-creator modify <section>
/exasol-developer-guide-creator implement
```

| Subcommand         | Description                                                                                                                                           |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| `explore`          | Audit the existing doc structure, rate quality against the What→How→Benefits standard, do interactive Q&A, and produce a prioritised improvement plan |
| `new <topic>`      | Plan a brand-new section — searches docs.exasol.com, github.com/exasol, and PyPI, asks clarifying questions, outputs a full file/structure plan       |
| `modify <section>` | Plan changes to an existing section — reads current content, optionally researches updates online, Q&A to agree scope, outputs a per-file change list |
| `implement`        | Write the actual RST files to disk (requires a plan from `new` or `modify` earlier in the conversation)                                               |

## Workflow

```
# Document a new feature
/exasol-developer-guide-creator new kafka connector
  → review plan
  → /exasol-developer-guide-creator implement

# Improve an existing section
/exasol-developer-guide-creator modify UDF
  → review plan
  → /exasol-developer-guide-creator implement

# Full project audit
/exasol-developer-guide-creator explore
  → /exasol-developer-guide-creator new or modify
  → /exasol-developer-guide-creator implement
```

## Installation

### Via Claude Marketplace (recommended)

Run these two commands in Claude Code:

```
/plugin marketplace add exasol-labs/exasol-developer-guide-skills
/plugin install exasol-developer-guide-skills@exasol-developer-guide-skills
```

### Manual installation

1. Clone this repository and copy the folder into `~/.claude/skills/`:

   ```bash
   git clone https://github.com/exasol-labs/exasol-developer-guide-skills.git
   cp -r exasol-developer-guide-skills ~/.claude/skills/exasol-developer-guide-creator
   ```

2. Restart Claude Code — the skill will appear in your `/skills` list as `exasol-developer-guide-creator`.

## Project requirements

These skills are designed for a documentation project with the following structure:

```
your-project/
└── doc/
    ├── index.rst          ← top-level Sphinx toctree
    ├── connect_to_exasol/ ← example: connector section
    ├── gen_ai/            ← example: tutorial section
    └── ...
```

- **File format:** reStructuredText (`.rst`), rendered by Sphinx
- **Target audience:** Data professionals and developers
- **Content standard:** What → How (with code examples) → Benefits + Real-world use cases

## Customising for a different project

To point these skills at a different documentation project, update the `**Project path:**` line in each `SKILL.md` file inside the sub-skill folders.
