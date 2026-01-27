# Searchwave

AI research synthesis for Claude Code — quick lookups to deep multi-agent research with Opus.

## Requirements

- Claude Code with WebSearch tool access
- Works best with Sonnet 4 or Opus 4.5

## Commands

| Command | Time | What it does |
|---------|------|--------------|
| `/wave [topic]` | ~60s | Quick research — 3 searches, 3 fetches, Sonnet synthesis. No questions. |
| `/deepwave [topic]` | ~70s-10min | Deep research — asks depth/priority, Opus synthesis. 3 tiers. |
| `/deepwave-x10 [topic]` | ~90s | Experimental — 10 parallel searches instead of 6. |

## When to Use Which

| Situation | Use |
|-----------|-----|
| Quick context on unfamiliar topic | `/wave` |
| "What is X?" questions | `/wave` |
| Research for a decision | `/deepwave` Standard |
| Technical deep-dive | `/deepwave` Max |
| Fact-checking a claim | `/wave` first, `/deepwave` if ambiguous |

Start with `/wave`. If you need more depth, it'll be obvious.

## Installation

### Plugin Install (Recommended)

```bash
claude plugin marketplace add rowbradley/searchwave
claude plugin install searchwave
```

Restart Claude Code to load the plugin.

### Manual Install

```bash
git clone https://github.com/rowbradley/searchwave.git
cp -r searchwave/skills/wave ~/.claude/skills/
cp -r searchwave/skills/deepwave ~/.claude/skills/
```

Restart Claude Code to load skills.

## /wave — Quick Research (~60s)

Single orchestrator, 3 parallel searches, 3 parallel fetches, Sonnet synthesis.
No QA — runs immediately.

**Output:** 300-400 words with sources, inline citations, no AI fluff.

## /deepwave — Deep Research

Asks for depth before running:

| Tier | Time | Architecture |
|------|------|--------------|
| Quick | ~70s | Single orchestrator, Opus synthesis |
| Standard | ~90s | Single orchestrator, 6 searches, Opus synthesis |
| Max | ~5-10min | 3 parallel research agents, Opus evaluation + follow-up loop |

**Output:** Survey-style report with confidence assessment, inline citations,
source limitations noted. Max mode includes a "Go Deeper?" follow-up loop.

### Max Mode Architecture

```
┌─────────────────────────────────────────┐
│  /deepwave "topic" → Max mode           │
├─────────────────────────────────────────┤
│                                         │
│  Wave 1: 3 parallel research agents     │
│  ┌──────────┬──────────┬──────────┐     │
│  │ Agent A  │ Agent B  │ Agent C  │     │
│  │ Facts    │ How-to   │ Why      │     │
│  │ (what)   │ (how)    │ (why)    │     │
│  └────┬─────┴────┬─────┴────┬─────┘     │
│       └──────────┼──────────┘           │
│                  ▼                      │
│  Opus Evaluation (quality signals)      │
│       │                                 │
│       ├─ SUFFICIENT → Synthesize        │
│       └─ NEEDS_MORE → Wave 2 → Synth   │
│                                         │
│  Final: Opus synthesis with confidence  │
│  assessment + "Go Deeper?" loop         │
└─────────────────────────────────────────┘
```

## /deepwave-x10 — Experimental

Standard mode variant with 10 parallel searches instead of 6. Testing whether
more search diversity improves output quality. Compare against `/deepwave`
Standard mode.

## Design Principles

- **Survey voice** — report what was found, don't editorialize
- **Inline citations** — every claim attributed to source
- **Source limitations noted** — vendor reports flagged, small samples called out
- **No AI writing patterns** — no hyperbole, no dramatic reframes, numbers first
- **Terminal-native** — hard-wrapped at 80 cols for readability

## License

MIT
