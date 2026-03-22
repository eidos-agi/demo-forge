# demo-clean — Clean Up Intermediate Demo Files

Remove intermediate recording files and ensure demo artifacts are properly gitignored.

## Trigger

User says `/demo-clean` or asks to clean up demo files, remove .cast files, or tidy the demo directory.

## Instructions

### Step 1: Find Intermediate Files

Check the `demo/` directory for files that should not be committed:

| File Type | Why Remove |
|-----------|-----------|
| `*.cast` | asciinema recordings — large, binary-ish, only needed during conversion |
| `*.html` | Social card HTML templates — intermediate, the PNG is the output |
| `*.mmd` | Mermaid source — keep if useful, but the SVG is the output |

### Step 2: Check .gitignore

Read `.gitignore` and check if demo intermediates are covered. If not, suggest adding:

```
# Demo intermediates
demo/*.cast
```

### Step 3: Report

```
## Demo Cleanup: {{PROJECT_NAME}}

| File | Size | Action |
|------|------|--------|
| demo/demo.cast | 245KB | Delete (intermediate) |
| demo/social-card.html | 3KB | Keep or delete (template) |

Suggested .gitignore additions:
  demo/*.cast
```

### Step 4: Clean

After user confirms:
- Delete intermediate files
- Update .gitignore if needed
- `git add .gitignore && git rm --cached demo/*.cast` if they were already tracked

## Rules

- **Always ask before deleting.** Show what will be removed and get confirmation.
- **Never delete final outputs** (GIFs, SVGs, PNGs) — only intermediates.
- **Keep .mmd files** unless user explicitly asks to remove them — they're useful for regeneration.
