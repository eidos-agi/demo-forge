# demo-forge

AI-generated demos for open-source software. Built by agents, not humans.

## Why?

The #1 conversion element in a GitHub README is a demo. Repos with demos get ~42% more stars. But recording, editing, and optimizing demos is tedious human work — exactly the kind of work agents should do.

demo-forge reads your project, identifies the hero feature, writes a demo script, records it, and produces a README-ready GIF, SVG, screenshot, or social card.

## Skills

| Skill | What |
|-------|------|
| `/demo` | Auto-generate demo content — terminal GIFs/SVGs, screenshots, architecture diagrams, social cards |
| `/demo-audit` | Audit existing demo quality — freshness, file size, positioning, hero feature coverage |
| `/demo-clean` | Remove intermediate files (.cast) and update .gitignore |

## Supported Formats

| Format | Best For | Tool Chain |
|--------|----------|------------|
| Terminal GIF | CLI tools, MCP servers | asciinema → agg |
| Terminal SVG | Same, crisper + smaller | asciinema → svg-term-cli |
| Screenshot PNG | Library output, APIs | Playwright |
| Architecture diagram | System design | Mermaid → SVG |
| Social card | Link previews (Open Graph) | HTML → Playwright |

## Usage

Clone alongside your projects:

```bash
git clone https://github.com/eidos-agi/demo-forge.git ~/repos-eidos-agi/demo-forge
```

Copy skills into any project:

```bash
cp ~/repos-eidos-agi/demo-forge/.claude/skills/demo*.md .claude/skills/
```

Then run `/demo` in that project.

## Part of the Forge Ecosystem

- [forge-forge](https://github.com/eidos-agi/forge-forge) — the meta-forge (create and manage forges)
- [foss-forge](https://github.com/eidos-agi/foss-forge) — FOSS standards and marketing
- [demo-forge](https://github.com/eidos-agi/demo-forge) — this repo
- [test-forge](https://github.com/eidos-agi/test-forge) — testing standards

## License

MIT — [Eidos AGI](https://github.com/eidos-agi)
