---
name: wavedeep-x10
description: "EXPERIMENTAL: Standard mode with 10 parallel searches (vs 6). Testing if more searches = better coverage."
user-invocable: true
---

# Searchwave Deep X10 (Experimental)

Standard mode variant with 10 parallel searches instead of 6. Testing hypothesis
that more search diversity improves output quality.

## When to Use

**Use /wavedeep-x10 when:**
- A/B testing against standard `/wavedeep` Standard mode
- Want to see if 10 searches provides better coverage

**Compare results to:** `/wavedeep` with Standard tier selected

---

## Execution

Single orchestrator, Opus synthesis. Fixed at Standard tier.

Print banner:
```
╔═════════════════════════════════════════╗
║           S E A R C H W A V E           ║
║                · · · · ·                ║
║     Searching: 10 parallel queries      ║
╚═════════════════════════════════════════╝
```

### Phase 1: QA (~15 sec)

Use ONE AskUserQuestion call with 2-3 questions:

**Question 1 (only if needed): Clarification**
Include if query has ambiguity OR broad scope needing focus.

**Question 2: Length preference**
Always include:
```
"Preferred length?"

- 800 words — concise report
- 1200 words — comprehensive
- 1500 words — detailed deep-dive
```

**Question 3: Priority selection**
Always include, but GENERATE OPTIONS based on the specific query:
```
"What angle matters most?" (pick 1-2)

Generate 3-4 options relevant to THIS topic.
Always include one "Recent developments" option.
```

### Step 1: Search (10 parallel)

Fire 10 WebSearches in ONE message:
```
"$ARGUMENTS"
"$ARGUMENTS [user's first priority]"
"$ARGUMENTS [user's second priority, or 'explained' if only one selected]"
"$ARGUMENTS guide"
"$ARGUMENTS tutorial"
"$ARGUMENTS examples"
"$ARGUMENTS comparison"
"$ARGUMENTS interesting"
"$ARGUMENTS recent"
"$ARGUMENTS reddit"
```

### Step 2: Fetch (10 parallel)

From search results, pick 10 best URLs. Skip Wikipedia for fetching (403s — use search snippets instead).

Priority order:
1. gov/institutional, domain authorities
2. Quality blogs, practitioner content
3. Reddit/forums (real user experience)
4. News sites (recent)
5. Tutorials, examples

Fire 10 WebFetches in ONE message. Proceed with available if any fail.

### Step 3: Opus Synthesis

Spawn ONE Task with `model: opus` and `subagent_type: general-purpose`:

```
Research on "$ARGUMENTS" from web sources:

[Insert all fetched content and relevant search snippets]

User priorities: [from QA]
Target length: [user's length selection] words

---

Synthesize into a [length]-word report:

**Voice and approach:**
1. Survey voice — report what you found, present the landscape
2. Attempt neutrality — present information, let reader decide
3. Cut educational filler that doesn't serve the user's priorities
4. Keep hard numbers, specific protocols, concrete thresholds
5. Name frameworks or mental models when useful

**Inline citations (critical):**
Every statistic or factual claim must include source attribution inline:
- "According to McKinsey (2024)..."
- "One study found..."
Acknowledge source limitations when relevant.

**Avoid AI writing patterns:**
- No dramatic reframes ("It's not X, it's Y")
- No hyperbole words: "brutal", "game-changer"
- Let facts speak; don't editorialize
- Be concise, lead with numbers

**Line width formatting (critical for terminal readability):**
- Prose and bullet lists: hard-wrap at 80 columns
- Tables, code blocks, diagrams: NO width limit

Output format:
# [Topic] Research Report

## Summary
[3-4 sentences. What we found, not what we conclude.]

## [Section titles as appropriate — don't force structure]
[Content with inline citations, organized by what's most useful]

## Sources
[Deduplicated, one-line descriptions]

*Searchwave Deep (X10) · [N] sources*
```

---

## Testing Notes

**Compare against:** `/wavedeep` Standard mode (6 searches, 6 fetches)

**Metrics to track:**
- Time to completion
- Number of successful fetches (out of 10)
- Source diversity (unique domains)
- Output quality (subjective)
- Any OOM or fetch failures

**Log results to:** `Personal/Projects/Context/Development.md`
