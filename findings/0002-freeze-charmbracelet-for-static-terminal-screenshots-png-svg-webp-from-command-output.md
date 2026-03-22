---
id: '0002'
title: >-
  Freeze (Charmbracelet) for static terminal screenshots — PNG/SVG/WebP from
  command output
status: open
evidence: HIGH
sources: 1
created: '2026-03-22'
---

## Claim

Freeze (charmbracelet/freeze) generates static screenshots (PNG, SVG, WebP) from terminal output. It's the complement to VHS: VHS for animated demos, Freeze for static screenshots.

**Key features:**
- `freeze --execute "aad checkup"` captures ANSI output directly
- Pipe support: `aad checkup | freeze -o screenshot.png`
- Customizable: window chrome, padding, fonts, themes, line numbers
- Language auto-detection for code screenshots
- Works with tmux capture-pane for TUI screenshots

**When to use Freeze vs VHS:**
- Freeze: static screenshots for README hero images, PyPI descriptions, social cards
- VHS: animated GIFs showing interactive workflows, multi-step demos

Both are from Charmbracelet, both work in CI, both are agent-friendly.

## Supporting Evidence

> **Evidence: [HIGH]** — https://github.com/charmbracelet/freeze, retrieved 2026-03-22

## Caveats

None identified yet.
