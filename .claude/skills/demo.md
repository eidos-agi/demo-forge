# demo — Generate Demo Content for a Project

The main skill. Reads the current project, identifies the hero feature, and produces publishable demo content — terminal recordings, screenshots, diagrams, or social cards.

## Trigger

User says `/demo` or asks to create a demo, GIF, recording, screenshot, or visual content for a project.

### Arguments

- No args: auto-detect project type and produce the best demo format
- `terminal` — terminal recording (GIF or SVG)
- `screenshot` — screenshot of output or interface
- `diagram` — architecture or data flow diagram
- `social-card` — Open Graph image for link previews
- `all` — generate all applicable demo types
- A description like `"show it handling 3 concurrent requests"` — custom scenario

## Instructions

### Step 1: Read the Project

Understand what to demo by reading:
- `README.md` — what it claims to do
- `pyproject.toml` — entry points, name, description
- Source code entry point — main module, CLI handler, MCP server definition
- Existing `demo/` directory — don't regenerate what already exists unless asked

Determine:
- **Project type**: CLI tool, MCP server, library, API, or other
- **Hero feature**: the single most compelling capability
- **Install method**: pip, pipx, uvx, brew
- **One-liner**: what makes someone care in ≤10 words

### Step 2: Choose Format

| Project Type | Primary Format | Secondary |
|-------------|---------------|-----------|
| CLI tool | Terminal GIF/SVG | Social card |
| MCP server | Terminal GIF showing tool invocation | Architecture diagram |
| Library | Code + output screenshot | Social card |
| API | Request/response flow diagram | Screenshot |
| Any | Social card for Open Graph | — |

### Prerequisites

Check for required tools before recording. Install what's missing:

| Tool | Needed For | Install |
|------|-----------|---------|
| `asciinema` | All terminal recordings | `pip install asciinema` |
| `agg` | GIF output | `cargo install --git https://github.com/asciinema/agg` |
| `svg-term-cli` | SVG output | `npm install -g svg-term-cli` |
| `playwright` | Screenshots, social cards | `pip install playwright && playwright install chromium` |
| `mmdc` | Mermaid diagrams | `npm install -g @mermaid-js/mermaid-cli` |

Check availability before starting:
```bash
echo "asciinema: $(which asciinema || echo 'MISSING')"
echo "agg: $(which agg || echo 'MISSING')"
echo "svg-term: $(which svg-term || echo 'MISSING')"
```

If critical tools are missing, output the demo script and install instructions — don't block the user.

### Step 3: Generate the Demo

#### Terminal Recording (CLI tools, MCP servers)

1. **Write the demo script** at `demo/demo-script.sh`:
   - Install the tool in a temp venv (quick, don't linger)
   - Show the hero feature with real, compelling output
   - ≤30 seconds total. Show the wow moment in the first 10.
   - Include `sleep 0.3-0.5` between commands for readability
   - Use `echo` section headers sparingly: `echo "→ Running health check..."`
   - No errors. Test before recording.
   - **For tools with dual output modes** (pretty CLI + JSON): show BOTH in the demo. First the human-readable output (the "wow"), then the structured JSON output (proves it's agent-native). This demonstrates agentic-first design. Example sequence:
     ```bash
     echo "→ Human-friendly output:"
     aad checkup --min-severity warning
     sleep 1
     echo ""
     echo "→ Structured agent output:"
     aad checkup --json --fields severity,summary,fix | head -20
     ```

2. **Record**:
   ```bash
   # Check for tools
   which asciinema || pip install asciinema

   # Record
   asciinema rec demo/demo.cast \
     --command "bash demo/demo-script.sh" \
     --cols 80 --rows 24 \
     --overwrite
   ```

3. **Convert**:

   For GIF (larger, universal):
   ```bash
   # agg must be installed: cargo install --git https://github.com/asciinema/agg
   agg demo/demo.cast demo/demo.gif \
     --theme monokai --font-size 14 --speed 1.2
   ```

   For SVG (preferred — crisp, small, scalable):
   ```bash
   # npm install -g svg-term-cli
   cat demo/demo.cast | svg-term \
     --out demo/demo.svg \
     --window --width 80 --height 24 \
     --term iterm2 --profile monokai
   ```

4. **Optimize**: if GIF > 5MB, increase `--speed` or trim the script.

#### Screenshot (libraries, output)

1. Write a Python script that produces the compelling output
2. Run it and capture the terminal output
3. Use Playwright or a terminal-to-image tool to produce a clean PNG
4. Alternatively, use `rich` to render styled output and capture via `rich.console.Console.export_svg()`

#### Architecture Diagram (MCP servers, systems)

1. Generate a Mermaid diagram showing the key components and data flow
2. Write to `demo/architecture.mmd`
3. Convert to SVG: `mmdc -i demo/architecture.mmd -o demo/architecture.svg -t dark`
4. Or embed directly in README with ```mermaid code blocks (GitHub renders natively)

#### Social Card (Open Graph image)

1. Generate an HTML template at `demo/social-card.html`:
   - 1200x630px (Open Graph standard)
   - Project name in large text
   - One-liner description
   - Eidos AGI branding (dark background, clean typography)
   - Optional: terminal screenshot embedded
2. Screenshot with Playwright: `playwright screenshot demo/social-card.html demo/social-card.png --viewport-size=1200,630`
3. Reference in README or repo settings for link previews

### Step 4: Embed in README

Generate the markdown and show the user where to place it (after hero line and badges):

```markdown
<p align="center">
  <img src="demo/demo.gif" alt="{{PROJECT_NAME}} demo" width="700">
</p>
```

For social card, add to repo description or use `<meta>` tag guidance.

### Step 5: Output Summary

```
## Demo Generated: {{PROJECT_NAME}}

| Asset | Path | Size | Format |
|-------|------|------|--------|
| Terminal demo | demo/demo.gif | 1.2MB | GIF |
| Social card | demo/social-card.png | 85KB | PNG |

README embed markdown:
<copy-paste block>

Commit with: git add demo/ && git commit -m "docs: add demo content"
```

## File Structure

```
demo/
├── demo-script.sh      ← bash script that runs the demo
├── demo.cast            ← asciinema recording (intermediate, gitignored if large)
├── demo.gif or .svg     ← terminal recording for README
├── architecture.mmd     ← mermaid source (if applicable)
├── architecture.svg     ← rendered diagram (if applicable)
├── social-card.html     ← social card template (if applicable)
└── social-card.png      ← rendered social card (if applicable)
```

## Rules

- **Real output only.** Every frame must come from actual code execution. (GUARD-002)
- **≤30 seconds for recordings.** (GUARD-003)
- **Don't overwrite existing demos** unless explicitly asked.
- **Test the script before recording.** A broken demo is worse than no demo.
- **If recording tools aren't installed**, output the script + clear install instructions. Don't block.
- **Optimize for GitHub rendering.** GIFs under 5MB, SVGs preferred, PNGs for screenshots.
