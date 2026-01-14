# Searchwave

AI research synthesis for Claude Code — quick lookups to deep research with Opus.

## Installation

**Development (load on startup):**
```bash
claude --plugin-dir ~/Projects/searchwave
```

**Persistent (local marketplace):**
```bash
claude plugin marketplace add ~/Projects/searchwave
claude plugin install searchwave@searchwave
```

After either method, restart Claude Code to load commands.

## Commands

| Command | Time | Description |
|---------|------|-------------|
| `/wave [topic]` | ~60s | Quick research, no questions asked |
| `/wavedeep [topic]` | ~70s-10min | Deep research with depth selection |

## Skills

Skills can also be invoked automatically based on context:

- `searchwave:wave` — Triggers on "quick lookup", "fast research"
- `searchwave:wavedeep` — Triggers on "deep research", "comprehensive research"

## /wave (Quick Research)

Single orchestrator, 3 parallel searches, 3 parallel fetches, Sonnet synthesis.
No QA — just runs and returns results.

**Output:** 300-400 words with sources, inline citations, no AI fluff.

## /wavedeep (Deep Research)

Asks for depth and priority before running:

| Tier | Time | Architecture |
|------|------|--------------|
| Quick | ~70s | Single orchestrator, Opus synthesis |
| Standard | ~90s | Single orchestrator, more sources, Opus |
| Max | ~5-10min | 3 parallel agents, Opus evaluation, follow-up loop |

**Output:** Survey-style report with confidence assessment, inline citations,
source limitations noted.

## Development

This package follows the superpowers skill pattern:
- Commands are thin wrappers that invoke skills
- Skills contain full execution instructions
- Subagent prompts extracted to separate files

## License

MIT
