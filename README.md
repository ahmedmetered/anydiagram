# anydiagram

Architecture diagrams for any codebase, from the AI agent you already have.

anydiagram maps a codebase into layered Mermaid diagrams using perspective-
based recursive analysis: structure, data flow, dependencies, API surface,
domain concepts, deployment. Every element with internal structure becomes a
child diagram. Output lands in an `architecture/` folder as plain markdown +
Mermaid that renders on GitHub, with the source files cited in every diagram.

Adapted from the method in
[oh-my-mermaid](https://github.com/oh-my-mermaid/oh-my-mermaid) (MIT), as an
agent-native pack: no CLI, no viewer server, no account. The agent you
already run does the analysis and writes the files.

## Install

Copy `skill/` into your agent's skills folder (ZCode, Claude Code, Codex,
Cursor - any agent that reads `SKILL.md` files), or clone this repository
into it; the root `SKILL.md` makes it discoverable either way.

## Use

- "Map the architecture of this project"
- "Diagram how data flows through this codebase"
- "Refresh the architecture docs" (diff mode: updates only what changed)

## Files

```
skill/SKILL.md    the method: perspectives, recursion, output contract
```

## Credits and license

MIT. Method adapted from
[oh-my-mermaid](https://github.com/oh-my-mermaid/oh-my-mermaid) by the
oh-my-mermaid contributors. Independent project; not affiliated with or
endorsed by Anthropic or any agent vendor.
