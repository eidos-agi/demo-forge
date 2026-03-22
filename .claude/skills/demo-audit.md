# demo-audit — Assess Demo Quality for a Project

Check whether a project's demo content exists, is effective, and meets demo-forge standards.

## Trigger

User says `/demo-audit` or asks to review, assess, or check demo content for a project.

## Instructions

### Check for Demo Content

Look for demo assets in the current repo:

| Location | What to look for |
|----------|-----------------|
| `demo/` directory | GIFs, SVGs, PNGs, scripts, casts |
| `README.md` | Embedded images, asciinema links, GIFs |
| Root directory | `*.gif`, `*.svg`, `screenshot*`, `demo*` |
| `.github/` | Social card, Open Graph images |

### Evaluate What Exists

For each demo asset found:

| Check | Criteria |
|-------|---------|
| Exists | Is there any demo content at all? |
| Position | Is it above the fold in README (before install instructions)? |
| Size | GIF ≤5MB? PNG ≤1MB? |
| Duration | Recording ≤30 seconds? |
| Real output | Does the demo script run real code, or is output hardcoded? |
| Currency | Does the demo reflect the current version of the tool? Check if demo-script.sh still runs cleanly. Also: compare any version strings in demo-script.sh against `project.version` in pyproject.toml — if they differ, WARN as stale. |
| Hero feature | Does the demo show the most compelling capability, not just `--help`? |
| Format | Is the format optimal? (SVG > GIF for terminal, PNG for screenshots) |

### Report

```
## Demo Audit: {{PROJECT_NAME}}

| Check | Status | Detail |
|-------|--------|--------|
| Demo exists | PASS/FAIL | Found demo/demo.gif (1.2MB) |
| Above the fold | PASS/FAIL | Embedded at line 8 of README |
| File size | PASS/WARN | 4.8MB — close to 5MB limit |
| Duration | PASS/FAIL | 22 seconds |
| Real output | PASS/FAIL | demo-script.sh runs actual commands |
| Current | PASS/WARN | Script references v0.1.0, current is v0.3.0 |
| Hero feature | PASS/WARN | Shows --help instead of the main capability |
| Social card | FAIL | No Open Graph image |

### Recommendation
1. Re-record demo with current version
2. Show the health check output instead of --help
3. Generate a social card with /demo social-card
```

## Rules

- Read-only. Don't create or modify anything.
- If no demo exists, say so clearly and recommend `/demo` to create one.
- If a demo exists but is stale, flag it — stale demos erode trust.
- Test demo-script.sh if it exists (run in dry-run or check if commands are valid).
