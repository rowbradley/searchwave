# Searchwave

Searchwave is a context agent for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that gets you (and Claude) up to speed on anything in about 60 seconds. 

Think native Claude Code search, but better and more comprehensive. Think Deep Research, but more concise, useful, and right in your terminal and Claude Code workflow.

## How it works

Searchwave works best when configured as a /command in Claude Code, to easily invoke the different modes.

`/wave` runs 3 parallel web searches, selects the best sources, fetches their content, and synthesizes a cited summary. The whole process takes about 60 seconds with no configuration or follow-up questions.

`/deepwave` adds depth control. Before running, it asks how deep (Quick / Standard / Max) and what angle matters most. All tiers use Opus for synthesis. Max mode dispatches 3 parallel research agents, evaluates source quality, and supports iterative follow-up.

Output is structured for terminals: inline citations, survey voice, hard-wrapped at 80 columns.

### Use cases

- Check how a framework or library works before adopting it
- Compare tools or approaches with real data
- Verify technical requirements or compatibility
- Get up to speed on an unfamiliar topic mid-task
- A general web search replacement
- A skill for other agents to use when additional context is necessary outside of pre-trained data

## Installation

### Claude Code (via Plugin Marketplace)

Register the marketplace:

```
/plugin marketplace add rowbradley/searchwave
```

Install the plugin:

```
/plugin install searchwave@searchwave
```

Restart Claude Code after installing.

### Verify Installation

```
/help
```

You should see `/wave` and `/deepwave` in your available commands.

### Manual Install

```bash
git clone https://github.com/rowbradley/searchwave.git
cp -r searchwave/skills/wave ~/.claude/skills/
cp -r searchwave/skills/deepwave ~/.claude/skills/
```

## Commands

| Command | Time | Use when |
|---------|------|----------|
| `/wave [topic]` | ~60s | Quick context — get up to speed fast |
| `/deepwave [topic]` | 70s–10min | Deep evaluation — make a decision with real data |

Start with `/wave`. If you need more depth, it'll be obvious.

## /wave — Quick Context

3 parallel searches → 3 best sources fetched → Sonnet synthesis. No questions asked. You type, it runs.

**What you get:** 300–400 words, inline citations, survey voice. Hard-wrapped at 80 columns for terminal readability.

## /deepwave — Deep Evaluation

Asks two things before running: how deep, and what angle matters most.

| Tier | Time | Architecture |
|------|------|--------------|
| Quick | ~70s | 3 searches, Opus synthesis |
| Standard | ~90s | 6 searches, Opus synthesis |
| Max | ~5–10min | 3 parallel research agents → Opus evaluation → follow-up loop |

**What you get:** Survey-style report with inline citations, source quality notes, and confidence assessment. Max mode adds a "Go Deeper?" loop for iterative exploration.

### How Max Mode Works

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

- **Survey voice** — reports what was found, doesn't editorialize
- **Inline citations** — every claim attributed to its source
- **Source quality awareness** — vendor reports flagged, limitations noted
- **No AI writing patterns** — no hyperbole, no reframes, numbers first
- **Terminal-native** — hard-wrapped at 80 columns

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) with WebSearch access
- Works best with Sonnet 4 or Opus 4.5

## Experimental

`/deepwave-x10` — Standard mode with 10 parallel searches instead of 6. Testing whether more search diversity improves coverage.

## License

MIT
