# Searchwave

Research from your terminal. Type `/wave sleep optimization` and get a cited
summary in 60 seconds. Need more? `/deepwave` runs multi-agent research with
quality evaluation and Opus synthesis.

A plugin for [Claude Code](https://docs.anthropic.com/en/docs/claude-code),
Anthropic's CLI for Claude.

## Commands

| Command | Time | What it does |
|---------|------|--------------|
| `/wave [topic]` | ~60s | Quick research. No questions asked. |
| `/deepwave [topic]` | 70s–10min | Deep research with depth and priority selection. |

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

Restart Claude Code after installing.

### Manual Install

```bash
git clone https://github.com/rowbradley/searchwave.git
cp -r searchwave/skills/wave ~/.claude/skills/
cp -r searchwave/skills/deepwave ~/.claude/skills/
```

## How /wave Works

3 parallel web searches → 3 best URLs fetched → Sonnet synthesis.
No questions, no configuration. You type, it runs.

**Output:** 300–400 words, inline citations, survey voice. Hard-wrapped
at 80 columns for terminal readability.

## How /deepwave Works

Asks two things before running: how deep, and what angle matters most.

| Tier | Time | Architecture |
|------|------|--------------|
| Quick | ~70s | 3 searches, Opus synthesis |
| Standard | ~90s | 6 searches, Opus synthesis |
| Max | ~5–10min | 3 parallel research agents → Opus evaluation → follow-up loop |

**Output:** Survey-style report with inline citations, source quality
notes, and confidence assessment. Max mode adds a "Go Deeper?" loop
for iterative exploration.

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

## Design Principles

- **Survey voice** — report what was found, don't editorialize
- **Inline citations** — every claim attributed to its source
- **Source limitations noted** — vendor reports flagged, small samples called out
- **No AI writing patterns** — no hyperbole, no dramatic reframes, numbers first
- **Terminal-native** — hard-wrapped at 80 columns for readability

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) with WebSearch access
- Works best with Sonnet 4 or Opus 4.5

## Experimental

`/deepwave-x10 [topic]` — Standard mode variant with 10 parallel searches
instead of 6. Testing whether more search diversity improves output quality.
Compare against `/deepwave` Standard.

## License

MIT
