# Searchwave

AI research synthesis for Claude Code — quick lookups to deep research with Opus.

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

## License

MIT
