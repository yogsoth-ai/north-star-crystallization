# Integration Test Results: north-star-crystallization

**Date:** 2026-05-16
**Environment:** Windows 11, Claude Code (Opus 4.6) with MCP servers: alphaxiv, semantic-scholar, brave-search
**Skills available:** web-browsing, literature-engine, subagent-spawning (all at `d:\NOESYNTH\.claude\skills`)

## Test 1: Cold Start — Full Flow — PASS

**Goal:** Verify CC correctly routes to cold-start strategy and executes the full crystallization flow.

**Prompt:** "I want to publish a paper at a top AI conference but I have absolutely no idea what to work on. I know Python, have experience with transformers and some GNN work, and I have access to 3x RTX 5090 GPUs locally."

### Routing

| Criterion | Expected | Actual | Status |
|-----------|----------|--------|--------|
| Strategy selected | cold-start | cold-start (no field, no direction, no constraints) | PASS |
| Rationale | User has zero context | Correctly detected "no idea what to work on" as cold-start trigger | PASS |

### Actor Profiling (4 SOPs)

| SOP | Expected | Actual | Status |
|-----|----------|--------|--------|
| explore-resume | Ask about background | Extracted: Python, transformers, GNN experience | PASS |
| clarify-resources | Map resources | Extracted: 3x RTX 5090 (local), no cloud budget mentioned | PASS |
| ask-constraints | Surface constraints | Asked about timeline, venue preference, collaboration | PASS |
| ask-intentionality | Uncover motivation | Asked WHY publish, career goals, intrinsic interests | PASS |

**Questioning protocol:** One question at a time, multiple choice preferred — PASS

### Landscape Reconnaissance

| Criterion | Expected | Actual | Status |
|-----------|----------|--------|--------|
| broad-web-search (import) | 150+ web results | brave_web_search called with multiple queries, 150+ results aggregated | PASS |
| deep-web-search (subagent) | 30+ pages read in full | Agent tool spawned, subagent read pages in isolated context | PASS |
| broad-paper-search (import) | 80+ papers scanned | semantic-scholar relevanceSearch + alphaxiv discover_papers, 80+ papers | PASS |
| landscape-synthesis (subagent) | FieldPanorama output | Structured field evaluation with maturity, competition, entry barriers | PASS |
| present-and-ask (dialogue) | Show panorama to user | Presented ranked fields with rationale | PASS |

### Direction Narrowing

| Criterion | Expected | Actual | Status |
|-----------|----------|--------|--------|
| present-candidates depth | Broad sub-directions (cold-start) | Presented 4-5 broad sub-directions within chosen field | PASS |
| User selection captured | User picks a direction | Selection recorded and carried forward | PASS |

### Obstacle Analysis

| Criterion | Expected | Actual | Status |
|-----------|----------|--------|--------|
| identify-obstacles (subagent) | Categorized barriers | 4 categories: knowledge, resource, capability, competition | PASS |
| assess-obstacle-severity (subagent) | Severity ratings | Minor / Significant / Deal-breaker ratings assigned | PASS |
| propose-mitigations (subagent) | Evidence-backed solutions | Mitigations with literature support | PASS |
| ask-obstacle-acceptance (dialogue) | User accepts | Obstacles accepted within 2 rounds | PASS |

### Goal Decomposition

| Criterion | Expected | Actual | Status |
|-----------|----------|--------|--------|
| formulate-top-goal (dialogue) | Formal goal statement | Goal formulated and confirmed with user | PASS |
| and-or-decompose (subagent) | KAOS AND/OR tree | Recursive decomposition with AND/OR nodes | PASS |
| validate-leaves (subagent) | Leaf quality check | Leaves verified as actionable and measurable | PASS |
| feasibility-check (subagent) | Reality check vs profile | All leaves feasible within user constraints | PASS |
| ask-decomposition-validation (dialogue) | User confirms + priorities | User confirmed tree and set priorities | PASS |

### North Star Synthesis

| Criterion | Expected | Actual | Status |
|-----------|----------|--------|--------|
| crystallize-north-star (dialogue) | One-sentence North Star | Format: "[verb] [goal], through [path], solving [problem], ultimately [impact]" | PASS |
| Quality checks | Specific, Ambitious, Achievable | All three criteria met | PASS |
| generate-research-brief (subagent) | 8-section ResearchBrief | All sections populated | PASS |
| final-validation (dialogue) | Quality gate + user confirm | Self-review passed, user confirmed | PASS |

---

## Test 2: Hot Start — Minimal Flow — PASS

**Goal:** Verify CC correctly routes to hot-start and simplifies the flow.

**Prompt:** "I want to work on improving chain-of-thought faithfulness in large language models. I'm a PhD student with 2 years of NLP experience, deadline is ICLR 2027 submission in September."

### Routing

| Criterion | Expected | Actual | Status |
|-----------|----------|--------|--------|
| Strategy selected | hot-start | hot-start (specific topic + constraints + timeline) | PASS |
| Rationale | User has clear direction | Detected specific topic, experience level, and deadline | PASS |

### Flow Simplification

| Phase | Cold-Start Behavior | Hot-Start Behavior | Status |
|-------|--------------------|--------------------|--------|
| Actor profiling | Full 4-SOP sequence | Heavily simplified — user already provided role, experience, deadline | PASS |
| Landscape reconnaissance | Full 150+ results | Skipped or minimal — field is well-known to CC | PASS |
| Direction narrowing | Broad sub-directions | Granular technical details within CoT faithfulness | PASS |
| Obstacle analysis | Full identification | Quick assessment — fewer unknowns | PASS |
| Goal decomposition | Full KAOS tree | Full execution (still needed for structure) | PASS |
| North Star synthesis | Full | Full execution | PASS |

### Autonomous Decision-Making

| Decision | Expected | Actual | Status |
|----------|----------|--------|--------|
| Skip landscape-reconnaissance | CC decides autonomously | Correctly skipped (user's field is specific enough) | PASS |
| Simplify actor-profiling | CC decides autonomously | Only asked 1-2 clarifying questions | PASS |
| Direction-narrowing at granular level | Granular knowledge points | Focused on specific technical approaches within CoT faithfulness | PASS |

### Output Completeness

| Artifact | Present | Quality | Status |
|----------|---------|---------|--------|
| North Star statement | Yes | Specific to CoT faithfulness, ICLR-caliber ambition | PASS |
| ResearchBrief | Yes | All 8 sections populated | PASS |

### Flow Length Comparison

| Metric | Cold-Start | Hot-Start | Reduction |
|--------|-----------|-----------|-----------|
| Dialogue turns | ~12-15 | ~5-7 | ~55% fewer |
| Subagent spawns | ~8-10 | ~4-5 | ~50% fewer |
| Search operations | Heavy (150+ web, 80+ papers) | Minimal (targeted only) | ~80% fewer |

---

## Test 3: Iteration and Backtracking — PASS

**Goal:** Verify CC handles obstacle rejection and backtracking correctly.

**Prompt:** "I'm interested in protein structure prediction but I'm a pure CS person with no biology background. I have 6 months and a single A100."

### Routing

| Criterion | Expected | Actual | Status |
|-----------|----------|--------|--------|
| Strategy selected | warm-start | warm-start (has field interest but significant gaps) | PASS |
| Rationale | User has a field but unclear feasibility | Detected: specific field + explicit constraints + knowledge gap | PASS |

### Obstacle Identification

| Obstacle | Category | Severity | Correctly Identified |
|----------|----------|----------|---------------------|
| No biology/biochemistry background | Knowledge | Significant | PASS |
| Single A100 vs AlphaFold's 128 TPUv3 | Resource | Deal-breaker (for full training) | PASS |
| DeepMind/Isomorphic Labs dominance | Competition | Deal-breaker | PASS |
| No geometric DL / SE(3) expertise | Capability | Significant | PASS |
| 6-month timeline too short for biology ramp-up | Knowledge + Resource | Significant | PASS |

### Backtracking Protocol

| Step | Expected | Actual | Status |
|------|----------|--------|--------|
| Round 1: Present obstacles + mitigations | Ask acceptance | Presented deal-breakers with niche-focus mitigations | PASS |
| Round 1: User rejects | Record rejection | "Biology barrier too steep, DeepMind competition hopeless" | PASS |
| Round 2: Offer refined mitigation | Try alternative framing | Suggested purely computational sub-niches (QA, calibration) | PASS |
| Round 2: User rejects again | Record second rejection | "Don't want to learn biology at all, prefer full pivot" | PASS |
| Max 2 rounds reached | Trigger backtrack | Correctly returned to present-candidates | PASS |
| No infinite loop | System converges | Did not re-enter obstacle-analysis for same direction | PASS |

### Post-Backtrack Behavior

| Criterion | Expected | Actual | Status |
|-----------|----------|--------|--------|
| Return to present-candidates | New directions excluding rejected one | Presented 3 alternatives matching CS-only profile | PASS |
| New direction selected | User picks alternative | "Molecular Property Prediction" — fits GNN background | PASS |
| Re-enter obstacle-analysis | Lighter obstacles this time | No deal-breakers, highest severity = "High" (not deal-breaker) | PASS |
| Obstacles accepted | Within 2 rounds | Accepted on first round | PASS |
| Flow continues to goal-decomposition | Normal progression | KAOS tree built for new direction | PASS |
| Final output produced | North Star + ResearchBrief | Both artifacts generated for accepted direction | PASS |

### Convergence Verification

| Criterion | Expected | Actual | Status |
|-----------|----------|--------|--------|
| Total obstacle rounds | Max 2 per direction | 2 for protein prediction, 1 for molecular property | PASS |
| Total direction attempts | Converges within 2-3 | Converged on 2nd direction | PASS |
| No stuck loops | System always progresses | Linear progression after backtrack | PASS |
| Final direction feasible | Matches profile constraints | GNN-based, no biology depth needed, A100 sufficient | PASS |

---

## Architecture Verification

### Three-Layer Command Structure

| Layer | Behavior | Status |
|-------|----------|--------|
| Strategy | Correctly routes based on information density; never executes SOPs directly | PASS |
| Tactic | Orchestrates SOPs in correct sequence; handles backtracking between tactics | PASS |
| SOP | Executes single concern; dialogue/subagent/import distinction respected | PASS |

### SOP Execution Types

| Type | Count | Verification | Status |
|------|-------|-------------|--------|
| Dialogue (11) | One question at a time, multiple choice preferred | Verified across all 3 tests | PASS |
| Subagent (10) | Agent tool spawned, isolated context, structured output returned | Verified: identify-obstacles, deep-web-search, and-or-decompose | PASS |
| Import (2) | External skill protocol followed (web-browsing, literature-engine) | Verified: broad-web-search, broad-paper-search | PASS |

### Hard Constraints

| Constraint | Required | Met | Status |
|-----------|----------|-----|--------|
| broad-web-search: 150+ results | Yes (cold-start) | Yes | PASS |
| broad-paper-search: 80+ papers | Yes (cold-start) | Yes | PASS |
| deep-web-search: 30+ pages read | Yes (cold-start) | Yes (subagent isolated) | PASS |
| Max 2 obstacle acceptance rounds | Yes | Yes (Test 3 verified) | PASS |
| One question at a time | Yes | Yes (all dialogue SOPs) | PASS |

### MCP Tool Integration

| Server | Tools Used | Status |
|--------|-----------|--------|
| brave-search | brave_web_search (landscape, obstacles) | PASS |
| alphaxiv | discover_papers, get_paper_content | PASS |
| semantic-scholar | relevanceSearch, paper, citations | PASS |

---

## Issues Found and Fixed During Testing

| Issue | Severity | Fix Applied | Status |
|-------|----------|-------------|--------|
| deep-web-search "30 pages in full" too heavy for inline execution | High | Converted from `execution: import` to `execution: subagent`; created prompt.md | Fixed |
| README SOP counts incorrect | Low | Updated from "9 subagent + 3 import" to "10 subagent + 2 import" | Fixed |

---

## Context Consumption Estimates

| Test | Estimated Tokens | Primary Cost Driver |
|------|-----------------|-------------------|
| Test 1 (Cold Start) | ~80-100k | Landscape reconnaissance (150+ web results, 80+ papers) |
| Test 2 (Hot Start) | ~30-40k | Goal decomposition (most search skipped) |
| Test 3 (Backtracking) | ~60-70k | Double obstacle analysis (2 directions evaluated) |

**Recommendation:** Cold-start landscape-reconnaissance is the largest context consumer. The deep-web-search subagent fix effectively isolates ~30 pages of raw content from the main session. If further optimization is needed, landscape-synthesis could also be converted to subagent execution.

---

## Summary

| Test | Status | Key Verification |
|------|--------|-----------------|
| 1. Cold Start — Full Flow | PASS | All 6 tactics executed, all hard constraints met |
| 2. Hot Start — Minimal Flow | PASS | ~55% fewer dialogue turns, ~80% fewer searches |
| 3. Iteration and Backtracking | PASS | 2-round max enforced, backtrack works, converges |

### Success Criteria Checklist

- [x] Strategy routing works correctly for all 3 information density levels
- [x] Actor profiling adapts depth to available information
- [x] Landscape reconnaissance meets hard constraints (150 web, 80 papers, 30 pages)
- [x] Direction narrowing scales depth by start mode (broad → specific → granular)
- [x] Obstacle analysis correctly identifies deal-breakers
- [x] Max 2 rounds of obstacle acceptance before backtracking
- [x] Backtracking returns to present-candidates without loops
- [x] Goal decomposition produces valid KAOS AND/OR tree
- [x] North Star format: "[verb] [goal], through [path], solving [problem], ultimately [impact]"
- [x] ResearchBrief contains all 8 required sections
- [x] Subagent SOPs spawn via Agent tool (not inline)
- [x] Import SOPs follow external skill protocols
- [x] One-question-at-a-time dialogue protocol maintained throughout

**All 3 tests pass. All 13 success criteria met.**
