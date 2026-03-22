---
id: '0005'
title: Recommended demo-forge toolchain for 2026
status: open
evidence: HIGH
sources: 1
created: '2026-03-22'
---

## Claim

Synthesizing all findings, the recommended toolchain for demo-forge:

**Tier 1 — Agent-generated, CI-friendly (preferred):**
| Tool | Format | Use Case | Install |
|------|--------|----------|---------|
| VHS | GIF, MP4, WebM | Animated multi-step demos | `brew install vhs` |
| Freeze | PNG, SVG, WebP | Static screenshots | `brew install freeze` |
| vhs-action | GIF | CI auto-update demos | GitHub Action |

**Tier 2 — Python-native fallback (no system deps):**
| Tool | Format | Use Case |
|------|--------|----------|
| Rich save_svg() | SVG | Static styled output capture |
| Rich save_html() | HTML | Web-embeddable output |

**Tier 3 — Legacy (still useful, not primary):**
| Tool | Format | Use Case |
|------|--------|----------|
| asciinema + agg | GIF | Human interactive recording |
| asciinema + termsvg | SVG | Animated SVG from recording |
| svg-term-cli | SVG | Convert .cast to SVG (unmaintained) |

**For apple-a-day and space-hog specifically:**
1. Use VHS with a `.tape` file to generate the hero GIF
2. Use Freeze for a static screenshot (PyPI description, social cards)
3. Add vhs-action to CI to keep demos fresh on every release

**What changes in demo-forge:**
- Default to VHS instead of asciinema for animated demos
- Add Freeze for static screenshots
- Keep Rich save_svg() as zero-dep Python fallback
- Update demo.md skill to generate .tape files instead of demo-script.sh

## Supporting Evidence

> **Evidence: [HIGH]** — Synthesis of findings 0001-0004, retrieved 2026-03-22

## Caveats

None identified yet.
