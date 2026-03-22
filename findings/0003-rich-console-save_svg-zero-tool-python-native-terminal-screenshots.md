---
id: '0003'
title: Rich console.save_svg() — zero-tool Python-native terminal screenshots
status: open
evidence: HIGH
sources: 1
created: '2026-03-22'
---

## Claim

Rich (Python) has built-in SVG export: `Console(record=True)` + `console.save_svg("output.svg")`. This captures styled terminal output as a crisp SVG without any external tools.

**How it works:**
```python
from rich.console import Console
console = Console(record=True)
console.print(table)
console.save_svg("demo.svg", title="apple-a-day checkup")
```

**Advantages:**
- Zero external tools — just Python + rich
- Perfect for libraries that already use rich for output
- Captures exact Rich styling (tables, colors, icons)
- Customizable themes via `rich.terminal_theme`
- SVG width matches terminal width, height auto-scales

**Limitations:**
- Only works if the tool uses Rich for output (not raw ANSI)
- Static only — no animation
- Requires `rich` as a dependency (though apple-a-day has it as optional)

**For demo-forge:** This is the ideal fallback when VHS/Freeze aren't installed. An agent can `pip install rich`, run the tool with Rich output, and capture an SVG — all in pure Python, no system deps.

## Supporting Evidence

> **Evidence: [HIGH]** — https://www.willmcgugan.com/blog/tech/post/exporting-svgs-of-terminal-output-with-rich/, https://rich.readthedocs.io/en/stable/console.html, retrieved 2026-03-22

## Caveats

None identified yet.
