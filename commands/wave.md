---
description: "Quick web research (~60 sec) - fast lookups, Opus synthesis"
---

# Searchwave

Topic: **$ARGUMENTS**

Quick web research synthesis in ~60 seconds.

## Execution

**Complete in 60 seconds. Dense facts, not fluff.**

### Step 0: Print banner

Print this banner immediately:
```
╔═════════════════════════════════════════╗
║           S E A R C H W A V E           ║
║                · · · · ·                ║
║      Searching: 3 parallel queries      ║
╚═════════════════════════════════════════╝
```

### Step 1: Search (3 parallel)

Fire 3 WebSearches in ONE message:
```
"$ARGUMENTS"              → baseline
"$ARGUMENTS interesting"  → non-obvious angles
"$ARGUMENTS guide"        → actionable content
```

All searches use `blocked_domains: ["medium.com"]` — Medium never fetches usefully.

### Step 2: Curate (10 sec)

Pick 3 URLs. Prefer: gov/institutional, domain authorities, quality blogs.

Skip for fetching:
- Wikipedia (403s — use snippet from search results instead)
- Medium (blocked at search level — never useful)
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

End with: `*Searchwave · [N] sources*` (where N is the number of sources fetched)
