---
name: anydiagram
description: >-
  Map any codebase into layered Mermaid architecture diagrams: perspective-
  based recursive analysis that produces a structure graph, data flow,
  dependency view, and per-module deep dives, written into an architecture/
  folder and updated as the code changes. Use when the user asks to diagram,
  map, or document a codebase's architecture, explain how a project is
  structured, or refresh architecture diagrams.
---

# anydiagram

Perspective-based architecture mapping, adapted from the method in
[oh-my-mermaid](https://github.com/oh-my-mermaid/oh-my-mermaid) (MIT). A
perspective is one distinct way of looking at a codebase. Each perspective
becomes one Mermaid diagram. Every element that has internal structure is
analyzed recursively and becomes a child diagram; leaves stay leaves. The
filesystem is the table of contents.

## Output contract

All output goes to an `architecture/` folder at the project root:

```
architecture/
  index.md              table of contents, mermaid master graph, changelog
  structure.md          components and their relationships
  data-flow.md          how information moves through the system
  dependencies.md       external packages, services, integrations
  api-surface.md        what the codebase exposes (only if API surface was selected)
  domain-concepts.md    core entities and rules (only if domain concepts were selected)
  deployment.md         where it runs (only if deployment was selected)
  <module>/             one subfolder per major module (recursive)
    overview.md         that module's diagram and notes
    <submodule>.md      recursive children
```

The three optional files exist only for the perspectives selected in Step 2 —
the contract now covers all six, so every selection has a defined output.
Diff-mode changelog entries live in `index.md` under a `## Changelog` section.

Conventions: diagram node IDs are English kebab-case and match folder names;
prose follows the user's configured language; every diagram is valid Mermaid
that renders on GitHub.

## Procedure

### Step 1: Explore

Read the manifests (package.json, pyproject.toml, go.mod, Cargo.toml,
pom.xml...), list top-level directories for module boundaries, read entry
points, and find route definitions, service layers, database connections,
and external integrations. Do not diagram from file names alone: read the
entry points.

### Step 2: Select perspectives

From the catalog, choose the perspectives that are meaningful for this
codebase - not all of them:

| Perspective | Answers | Diagram type |
|---|---|---|
| Structure | What are the components and how do they relate? | flowchart |
| Data flow | Where does data enter, transform, and land? | flowchart LR |
| Dependencies | What external things does it need? | graph |
| API surface | What does it expose? | flowchart |
| Domain concepts | What are the core entities and rules? | classDiagram |
| Deployment | Where does it run? | flowchart |

### Step 3: Recursive analysis

For each element in a diagram: if it has internal structure worth
explaining, it becomes a child element with its own diagram in its own
file. Recurse until the leaves are simple enough to be one bullet. Depth
beats width: five precise child diagrams beat one giant unreadable one.

### Step 4: Emit

Write the files. Every diagram starts with the perspective it answers and
ends with the evidence: which files and entry points the analysis read. A
diagram without cited sources is a guess, and guesses are marked as such.

### Step 5: Diff mode

When `architecture/` already exists, re-read the code, update only the
diagrams whose facts changed, and add a short changelog entry to index.md.
Never regenerate from zero: stale-but-cited diagrams are corrected, not
destroyed.
