---
name: wave
description: Quick web research (~60 sec) - fast lookups, synthesis. Use for "quick lookup", "fast research", or any topic needing quick context.
user-invocable: true
---

# Searchwave

Quick web research synthesis in ~60 seconds.

## Overview

Single orchestrator, 3 parallel searches, 3 parallel fetches. Produces a
300-400 word summary with sources. No questions asked — receives topic and
runs immediately.

## When to Use

**Use /wave when:**
- User asks for "quick lookup" or "fast research"
- Need context before a meeting or decision
- Simple factual questions
- Time-sensitive requests

**Use /wavedeep instead when:**
- User wants depth selection or priority focus
- Complex topics requiring multiple angles
- Need confidence assessment and source evaluation
- "Deep research" or "comprehensive" requests

## Execution

**Complete in 60 seconds. Dense facts, not fluff.**

### Step 0: Print banner

Print this colored ASCII banner immediately:
```
\033[36m ___  ___   _   ___  ___ _  ___      _____   _____ \033[0m
\033[34m/ __| __| /_\ | _ \/ __| || \ \    / /_\ \ / / __|\033[0m
\033[35m\__ \ _| / _ \|   / (__| __ |\ \/\/ / _ \ V /| _| \033[0m
\033[33m|___/___/_/ \_\_|_\___|_||_| \_/\_/_/ \_\_/ |___|  \033[0m
```

Then print status:
```
\033[36m╭─────────────────────────────────────────╮\033[0m
\033[36m│  SEARCHING: 3 parallel queries...       │\033[0m
\033[36m╰─────────────────────────────────────────╯\033[0m
```

### Step 1: Search (3 parallel)

Fire 3 WebSearches in ONE message:
```
"[topic]"              → baseline
"[topic] interesting"  → non-obvious angles
"[topic] guide"        → actionable content
```

### Step 2: Curate (10 sec)

Pick 3 URLs. Prefer: gov/institutional, domain authorities, quality blogs.

Skip for fetching:
- Wikipedia (403s — use snippet from search results instead)
- Paywalled sites
- SEO farms, outdated content

### Step 3: Fetch (3 parallel)

Fire 3 WebFetches in ONE message. Proceed with available if any fail.

### Step 4: Write

**Adapt structure to topic. No rigid template.**

Always include:
- **Overview** — 2-3 sentences, plain language
- **Key Findings** — Specific numbers, names, thresholds. This is the meat.
- **Sources** — With one-line descriptions

Include ONLY if warranted:
- **Practical Takeaways** — If topic has actionable advice
- **Of Interest** — ONLY if genuinely surprising. Skip if straightforward.
- **Go Deeper?** — ONLY if topic clearly warrants more research

**Style:**
- Concrete > abstract
- Numbers > vague claims
- Useful > clever
- Skip sections that don't add value
- ASCII tables/diagrams when helpful for comparisons
- No --- dividers between sections
- Tight, scannable organization
- Inline citations for statistics: "According to X...", "One study found..."

**Avoid AI writing patterns:**
- No dramatic reframes or hyperbole
- Let facts speak; don't editorialize
- Be concise, lead with numbers

**Line width formatting (critical for terminal readability):**
- Prose paragraphs: hard-wrap at 80 columns
- Bullet lists: hard-wrap at 80 columns
- Tables: NO width limit (columns break if wrapped)
- Code blocks: NO width limit
- ASCII diagrams: NO width limit

End with: `*Searchwave in [XX]s*`
