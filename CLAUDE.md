# CLAUDE.md — demo-forge

> AI-generated demos for open-source software. Videos, GIFs, images, and visual content — built by agents, not humans.

## What This Is

demo-forge creates demo content for FOSS projects. The agent reads the project, understands the hero feature, and produces publishable assets: terminal recordings, screenshots, diagrams, and social cards.

The founder shouldn't be making GIFs. The agent should.

## Skills

| Skill | What It Does |
|-------|-------------|
| `/demo` | Generate demo content — terminal GIFs, SVGs, screenshots, diagrams, social cards |
| `/demo-audit` | Assess existing demo content quality and freshness |
| `/demo-clean` | Remove intermediate files (.cast) and update .gitignore |

## Guardrails

1. **No software.** Skills and templates only.
2. **Real output only.** No faked or mocked demos. Every frame from actual code execution.
3. **30-second maximum.** Demos sell; tutorials teach.

## Related Forges

- **forge-forge** — meta-forge for creating and managing forges
- **foss-forge** — open-source standards and marketing. `/foss-demo` delegates here.
- **test-forge** — testing standards and test generation
