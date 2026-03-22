---
id: '0004'
title: 'SVG > GIF for GitHub READMEs — smaller, crisper, GitHub-native rendering'
status: open
evidence: MODERATE
sources: 1
created: '2026-03-22'
---

## Claim

SVG is the superior format for terminal demos on GitHub:

- **Crisp at any resolution** — vector, not raster. GIFs look blurry scaled up.
- **Smaller file size** — SVG terminal demos are typically 5-20x smaller than equivalent GIFs
- **GitHub renders SVGs natively** in README markdown
- **Animated SVGs work** on GitHub — CSS animations embedded in the SVG file itself
- **Copy-pasteable text** — users can select and copy text from SVG demos (impossible with GIFs)

**Platform support matrix:**
| Platform | GIF | Animated SVG | Static SVG | MP4/WebM |
|----------|-----|-------------|------------|----------|
| GitHub README | Yes | Yes (CSS anim) | Yes | No |
| PyPI | Yes | Partial | Yes | No |
| npm | Yes | Yes | Yes | No |
| Twitter/X | Yes | No | No | Yes |

**Recommendation for demo-forge:** Generate SVG as primary format (crisp, small, GitHub-native), GIF as fallback (universal compatibility, social media). VHS outputs GIF/MP4 natively; for SVG, use termsvg, svg-term-cli, or Rich's save_svg().

## Supporting Evidence

> **Evidence: [MODERATE]** — https://dev.to/brpaz/make-your-project-readme-file-stand-out-with-animated-gifs-svgs-4kpe, https://blog.eamonncottrell.com/animate-svgs-for-github-readmes, retrieved 2026-03-22

## Caveats

None identified yet.
