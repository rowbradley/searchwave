# Searchwave

AI research synthesis for Claude Code — quick lookups to deep research with Opus.

## Requirements

- Claude Code with WebSearch tool access
- Works best with Sonnet 4 or Opus 4.5

## When to Use Which

| Situation | Use |
|-----------|-----|
| Quick context on unfamiliar topic | `/wave` |
| "What is X?" questions | `/wave` |
| Research for a decision | `/wavedeep` Standard |
| Technical deep-dive | `/wavedeep` Max |
| Fact-checking a claim | `/wave` first, `/wavedeep` if ambiguous |

**Rule of thumb:** Start with `/wave`. If you need more depth, it'll be obvious.

## Installation

### Plugin Install (Recommended)

```bash
# Add as marketplace (one-time)
claude plugin marketplace add rowbradley/searchwave

# Install the plugin
claude plugin install searchwave
```

Restart Claude Code to load the plugin.

### Manual Install

Copy skills to your Claude Code skills directory:

```bash
# Clone repo
git clone https://github.com/rowbradley/searchwave.git

# Copy skills
cp -r searchwave/skills/wave ~/.claude/skills/
cp -r searchwave/skills/wavedeep ~/.claude/skills/
```

Restart Claude Code to load skills.

## Usage

| Command | Time | Description |
|---------|------|-------------|
| `/wave [topic]` | ~60s | Quick research, no questions asked |
| `/wavedeep [topic]` | ~70s-10min | Deep research with depth selection |
| `/wavedeep-x10 [topic]` | ~90s | Experimental: 10 parallel searches |

Skills are also auto-invoked by Claude when relevant to your task.

## /wave (Quick Research)

Single orchestrator, 3 parallel searches, 3 parallel fetches, Sonnet synthesis.
No QA — just runs and returns results.

**Output:** 300-400 words with sources, inline citations, no AI fluff.

## /wavedeep (Deep Research)

Asks for depth before running:

| Tier | Time | Architecture |
|------|------|--------------|
| Quick | ~70s | Single orchestrator, Opus synthesis |
| Standard | ~90s | Single orchestrator, more sources, Opus |
| Max | ~5-10min | 3 parallel agents, Opus evaluation, follow-up loop |

**Output:** Survey-style report with confidence assessment, inline citations,
source limitations noted.

## /wavedeep-x10 (Experimental)

Standard mode variant with 10 parallel searches instead of 6. Testing whether
more search diversity improves output quality. Compare against `/wavedeep`
Standard mode.

## Example Output

### /wave output (~300-400 words)

```
Query: "How does Cursor's AI agent handle multi-file edits?"

Cursor's AI agent uses a "composer" architecture that operates across
files simultaneously rather than sequentially [1]. When making multi-file
changes, it creates a unified diff plan, validates cross-file dependencies,
then applies changes atomically [2].

Key implementation details:
- AST-aware editing prevents syntax breaks across file boundaries
- Rollback support if any file edit fails
- Context window includes all affected files, not just the active one

The agent differs from Copilot's single-file focus by maintaining a
"workspace model" — a lightweight representation of project structure
that guides edit decisions [3].

**Sources:**
1. [Cursor Architecture Blog](https://cursor.sh/blog/architecture) — primary
2. [Anysphere Engineering](https://anysphere.inc/research) — implementation details
3. [Hacker News Discussion](https://news.ycombinator.com/item?id=...) — user reports
```

### /wavedeep output (~800-2500 words depending on depth)

Produces a structured research report with:
- Executive summary
- Detailed findings by theme
- Confidence assessment (high/medium/low per claim)
- Source quality notes
- Knowledge gaps identified
- Inline citations throughout

## License

MIT
