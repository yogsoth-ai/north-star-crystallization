# Integration Test: north-star-crystallization

Use this prompt in a Claude Code session within this repo to test the north-star skill against live MCP servers.

## Prerequisites

- brave-search MCP configured
- alphaxiv MCP configured (SSE: https://mcp.alphaxiv.org)
- semantic-scholar MCP configured (@yogsoth-ai/semantic-scholar-mcp)
- web-browsing repo available at sibling path
- literature-engine repo available at sibling path
- subagent-spawning repo available at sibling path

## Test 1: Cold Start — Full Flow

**Goal:** Verify CC correctly routes to cold-start strategy and executes the full crystallization flow.

**Prompt:**

```
Read skills/north-star/SKILL.md. I want to publish a paper at a top AI conference but I have absolutely no idea what to work on. I know Python, have experience with transformers and some GNN work, and I have access to 3x RTX 5090 GPUs locally. Help me figure out my research direction.
```

**Expected behavior:**
1. Routes to cold-start strategy
2. Begins actor-profiling (explore-resume → clarify-resources → ask-constraints → ask-intentionality)
3. Proceeds through landscape-reconnaissance with actual web searches (150+ results)
4. Narrows direction with paper search (80+ papers)
5. Identifies obstacles and proposes mitigations
6. Decomposes into GoalTree
7. Produces North Star + ResearchBrief

**Verify:**
- Questioning Protocol followed (one question at a time, multiple choice preferred)
- Subagent SOPs actually spawn agents (check Agent tool calls)
- Import SOPs follow external skill protocols
- Hard constraints met (150 web results, 80 papers, 30 web pages)

## Test 2: Hot Start — Minimal Flow

**Goal:** Verify CC correctly routes to hot-start and simplifies the flow.

**Prompt:**

```
Read skills/north-star/SKILL.md. I want to work on improving chain-of-thought faithfulness in large language models. I'm a PhD student with 2 years of NLP experience, deadline is ICLR 2027 submission in September. Help me structure this into a clear research goal.
```

**Expected behavior:**
1. Routes to hot-start strategy
2. Heavily simplified actor-profiling (user already provided most info)
3. May skip landscape-reconnaissance entirely
4. Direction-narrowing focuses on granular technical details within CoT faithfulness
5. Quick obstacle analysis
6. Goal decomposition into specific sub-goals
7. Produces North Star + ResearchBrief

**Verify:**
- Flow is significantly shorter than cold-start
- CC makes autonomous decisions about what to skip/simplify
- Final output is still complete (North Star + ResearchBrief)

## Test 3: Iteration and Backtracking

**Goal:** Verify CC handles obstacle rejection and backtracking correctly.

**Prompt:**

```
Read skills/north-star/SKILL.md. I'm interested in protein structure prediction but I'm a pure CS person with no biology background. I have 6 months and a single A100.
```

**Expected behavior:**
1. Routes to warm-start
2. During obstacle-analysis, identifies significant knowledge barriers (biology)
3. Proposes mitigations (courses, collaborators, computational-only approaches)
4. If user rejects obstacles, returns to present-candidates with alternative directions
5. Eventually converges on a feasible direction

**Verify:**
- Backtracking works (returns to earlier tactic when obstacles rejected)
- Maximum 2 rounds of obstacle acceptance before redirecting
- CC doesn't get stuck in loops
