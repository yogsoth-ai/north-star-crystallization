# north-star-crystallization

Goal-Driven Requirement Refinement Engine for Research — crystallize your North Star through adaptive dialogue and on-demand investigation.

## What This Does

Transforms fuzzy research intent into a crystallized **North Star** statement and structured **ResearchBrief** through adaptive dialogue and on-demand investigation (web search, paper search).

Works for users at any stage:
- **Cold start**: "I want to publish but have no idea what to research"
- **Warm start**: "I'm interested in LLM reasoning but nothing specific"
- **Hot start**: "I want to improve CoT faithfulness — help me structure this"

## Architecture

```
Entry Point (north-star/) → routes to strategy based on user's information density

Strategy (cold-start | warm-start | hot-start)
  → War doctrine + available tactics

Tactic (6): actor-profiling, landscape-reconnaissance, direction-narrowing,
            obstacle-analysis, goal-decomposition, north-star-synthesis
  → Methodology guidance + available SOPs

SOP (23): dialogue (11) | subagent (9) | import (3)
  → Specific techniques
```

This is a **strategy book (兵法书)**, not a pipeline. CC reads it and makes autonomous decisions about execution order, depth, and iteration.

## Theoretical Foundations

- **KAOS** (van Lamsweerde): Goal → Sub-goal → Obstacle → Resolution
- **i*** (Yu): Actor Modeling + Intentionality (WHY questions)
- **NFR Framework**: Softgoal decomposition for feasibility

## Output Artifacts

1. **North Star**: One sentence — "[verb] [goal], through [path], solving [problem], ultimately [impact]"
2. **ResearchBrief**: Structured context document for downstream research strategies

## Dependencies

- [web-browsing](https://github.com/NOESYNTH/web-browsing) — web search and research skills
- [literature-engine](https://github.com/NOESYNTH/literature-engine) — paper search and reading skills
- [subagent-spawning](https://github.com/NOESYNTH/subagent-spawning) — subagent dispatch conventions

## Usage

Invoke the `north-star` skill in a Claude Code session with MCP servers configured (brave-search, alphaxiv, semantic-scholar).
