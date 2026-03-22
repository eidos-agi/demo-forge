---
id: '0001'
title: >-
  VHS (Charmbracelet) is the best tool for agent-generated demos — declarative,
  CI-native, no interactive terminal needed
status: open
evidence: HIGH
sources: 1
created: '2026-03-22'
---

## Claim

VHS (charmbracelet/vhs, 15k+ stars) solves the exact problem we hit: it uses declarative `.tape` files instead of interactive recording. You write a script, VHS executes it in a virtual terminal and outputs GIF/MP4/WebM.

**Why it's the right choice for demo-forge:**
- **Declarative**: `.tape` files are text — agents can generate them programmatically
- **CI-native**: Official GitHub Action (`charmbracelet/vhs-action`) keeps demos up-to-date on every push
- **No interactive terminal**: runs headlessly, perfect for agent execution
- **Multiple outputs**: GIF, MP4, WebM from same tape file
- **Highly configurable**: fonts, themes, window chrome, padding, frame rate

**Tape file format:**
```
Output demo.gif
Set FontSize 14
Set Width 90
Set Height 24
Set Theme "Monokai"

Type "aad checkup --min-severity warning"
Enter
Sleep 5s
```

**Requirements**: ttyd + ffmpeg (both `brew install`-able)

**Comparison to asciinema**: asciinema requires a real PTY and hangs in non-interactive contexts (we experienced this). VHS creates its own virtual terminal. asciinema is better for human recording; VHS is better for programmatic/agent recording.

This should replace asciinema as demo-forge's primary recording tool.

## Supporting Evidence

> **Evidence: [HIGH]** — https://github.com/charmbracelet/vhs, https://github.com/charmbracelet/vhs-action, https://github.com/orangekame3/awesome-terminal-recorder, retrieved 2026-03-22

## Caveats

None identified yet.
