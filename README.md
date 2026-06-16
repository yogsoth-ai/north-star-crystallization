<!-- markdownlint-disable -->
<div align="center">

> *Research begins with a question — but the question itself must be discovered. Most researchers waste months wandering before finding their direction. This skill replaces wandering with structured crystallization.*

</div>

# 🔮 North Star Crystallization

*Goal-Driven Requirement Refinement Engine for Research*

Transforms fuzzy research intent into a crystallized **North Star** statement and structured **ResearchBrief** through adaptive dialogue and on-demand investigation. Not a chatbot that asks "what do you want to research?" — a structured coaching system that discovers the answer with you.

> 🧭 **Part of the [De-Anthropocentric Research Engine](https://github.com/yogsoth-ai/de-anthropocentric-research-engine).** This repository is one of nine composable research packages that make up DARE — the full autonomous research-orchestration system. DARE bundles this package together with the others into a single self-contained clone, unified under one orchestrator. To use these skills as intended — with the spec-driven orchestrator and cross-package routing — clone the [main repository](https://github.com/yogsoth-ai/de-anthropocentric-research-engine) rather than this repo alone.

---

## ⚡ What It Does

- 🎯 **Adaptive routing** — detects how much context you already have (cold/warm/hot) and adjusts depth accordingly. No wasted questions if you already know your direction.
- 🧑 **Actor profiling** — builds a structured model of WHO you are: skills, resources, constraints, values, motivations. Not a form — a dialogue.
- 🌍 **Landscape reconnaissance** — searches 150+ web results and 80+ papers to map the terrain of your chosen field. Evaluates maturity, competition, entry barriers.
- 🎯 **Direction narrowing** — presents ranked sub-directions within your field, matched to your specific profile. You choose; it doesn't choose for you.
- ⚔️ **Obstacle analysis** — identifies barriers (knowledge, resource, capability, competition), assesses severity, proposes evidence-backed mitigations. If obstacles are unacceptable, backtracks to alternative directions.
- 🌳 **Goal decomposition** — KAOS-style AND/OR tree decomposition of your top goal into actionable, verifiable sub-goals. Feasibility-checked against your profile.
- 💎 **North Star synthesis** — crystallizes everything into one sentence: "[verb] [goal], through [path], solving [problem], ultimately [impact]"
- 📋 **Research Brief generation** — aggregates all context into a structured document for downstream research strategies (e.g., DARE's intake)

---

## 🎯 Design Philosophy

### 🤔 Why Not Just Ask "What Do You Want to Research?"

Because most people don't know. And those who think they know often haven't validated their direction against reality — the field might be saturated, the barriers might be insurmountable, or a better direction might be hiding one step away.

North Star Crystallization treats research direction as a **requirements engineering problem**. The user is a stakeholder with fuzzy needs; the skill's job is to elicit, structure, validate, and crystallize those needs into actionable requirements.

### 📖 The Strategy Book Metaphor

This is not a pipeline. It's a **strategy book** — CC reads it and makes autonomous decisions about:
- Which tactics to deploy and in what order
- How deep to go (cold-start goes deep; hot-start skips most)
- When to backtrack (obstacles rejected → return to direction selection)
- When to iterate (goal decomposition fails validation → refine)

The human provides direction and decisions. The AI provides structure and investigation.

### 🎖️ Three-Layer Command Structure

```
Strategy (cold-start | warm-start | hot-start)
  → War doctrine: WHAT to accomplish, HOW MUCH depth
  → Available tactics + execution order guidance

Tactic (6 available)
  → Methodology: HOW to combine SOPs into coherent workflows
  → Available SOPs + sequencing logic

SOP (23 total: 11 dialogue + 10 subagent + 2 import)
  → Execution: HOW to do one specific thing
  → Either talks to user, spawns an agent, or imports external skill
```

Each layer has a single concern. A Strategy never executes an SOP directly. A Tactic never decides research direction. Strict layering = independently testable, replaceable, composable.

### 🧠 Theoretical Foundations

| Framework | What It Contributes | Where It Appears |
|-----------|-------------------|-----------------|
| **KAOS** (van Lamsweerde) | Goal → Sub-goal → Obstacle → Resolution | goal-decomposition tactic |
| **i*** (Yu) | Actor Modeling + Intentionality (WHY questions) | actor-profiling tactic |
| **NFR Framework** | Softgoal decomposition for feasibility | feasibility-check SOP |
| **Requirements Engineering** | Elicitation → Analysis → Specification → Validation | Overall flow structure |

---

## 🏗️ Architecture

```
┌───────────────────────────────────────────────────────────────┐
│  ENTRY POINT (ENTRY.md)                                       │
│  Routes to strategy based on user's information density       │
├───────────────────────────────────────────────────────────────┤
│  STRATEGY (3)                                                 │
│  cold-start, warm-start, hot-start                            │
├───────────────────────────────────────────────────────────────┤
│  TACTIC (6)                                                   │
│  actor-profiling, landscape-reconnaissance,                   │
│  direction-narrowing, obstacle-analysis,                      │
│  goal-decomposition, north-star-synthesis                     │
├───────────────────────────────────────────────────────────────┤
│  SOP (23)                                                     │
│  dialogue (11) | subagent (9) | import (3)                    │
├───────────────────────────────────────────────────────────────┤
│  EXTERNAL SKILLS (MCP servers — atomic operations)            │
│  brave-search, alphaxiv, semantic-scholar,                    │
│  web-browsing, literature-engine, subagent-spawning           │
└───────────────────────────────────────────────────────────────┘
```

### 📁 Repository Structure

All skills are **flat** under `skills/` — no nested `strategy/tactic/sop/` subdirectories. This means users can `cp -r skills/ ~/.claude/skills/` and immediately have all 33 skills available as `/` commands.

```
north-star-crystallization/
├── ENTRY.md                          # Root entry point
├── skills/
│   ├── north-star-crystallization/   # Campaign SKILL.md
│   │
│   │   # Strategies (3)
│   ├── cold-start/                   # Full flow for zero-context users
│   ├── warm-start/                   # Partial flow for users with some direction
│   ├── hot-start/                    # Minimal flow for users with clear direction
│   │
│   │   # Tactics (6)
│   ├── actor-profiling/              # WHO is the researcher
│   ├── landscape-reconnaissance/     # WHAT does the field look like
│   ├── direction-narrowing/          # WHERE specifically to go
│   ├── obstacle-analysis/            # WHAT stands in the way
│   ├── goal-decomposition/           # HOW to break it down
│   ├── north-star-synthesis/         # CRYSTALLIZE the final output
│   │
│   │   # SOPs — Dialogue (11)
│   ├── explore-resume/               # Understand background
│   ├── clarify-resources/            # Map available resources
│   ├── ask-constraints/              # Surface constraints
│   ├── ask-intentionality/           # Uncover motivations
│   ├── present-and-ask/              # Show panorama, gather preferences
│   ├── present-candidates/           # Show ranked sub-directions
│   ├── ask-obstacle-acceptance/      # User accepts or rejects obstacles
│   ├── formulate-top-goal/           # Formal goal statement
│   ├── ask-decomposition-validation/ # User confirms goal tree
│   ├── crystallize-north-star/       # Final one-sentence output
│   ├── final-validation/             # Quality gate + user confirm
│   │
│   │   # SOPs — Subagent (10)
│   ├── generate-candidate-fields/    # Generate field candidates
│   ├── landscape-synthesis/          # Evaluate fields → FieldPanorama
│   ├── deep-web-search/              # Full-page web reading (isolated context)
│   ├── identify-obstacles/           # Enumerate barriers
│   ├── assess-obstacle-severity/     # Rate obstacle difficulty
│   ├── propose-mitigations/          # Evidence-backed solutions
│   ├── and-or-decompose/             # KAOS goal tree
│   ├── validate-leaves/              # Leaf node quality check
│   ├── feasibility-check/            # Reality check vs profile
│   ├── generate-research-brief/      # Aggregate all context
│   │
│   │   # SOPs — Import (2)
│   ├── broad-web-search/             # → web-browsing/web-search
│   └── broad-paper-search/           # → literature-engine/literature-overview
├── tests/
│   └── integration-prompt.md   # Live integration test scenarios
└── README.md
```

Users can copy the entire `skills/` directory into their `.claude/skills/` to register all 33 skills as `/` commands.

---

## 🧩 Skill Inventory

### Strategies (3)

| Strategy | Trigger | Depth |
|----------|---------|-------|
| **cold-start** | User has no direction, no field, no constraints | Full: all 6 tactics, all SOPs, maximum search depth |
| **warm-start** | User has a field or vague direction | Moderate: skip/simplify actor-profiling, full landscape + obstacles |
| **hot-start** | User has specific topic + constraints | Minimal: quick profiling, skip landscape, focus on decomposition |

### Tactics (6)

| Tactic | Purpose | Key SOPs |
|--------|---------|----------|
| **actor-profiling** | Build structured model of the researcher | explore-resume, clarify-resources, ask-constraints, ask-intentionality |
| **landscape-reconnaissance** | Map the terrain of candidate fields | broad-web-search, deep-web-search, broad-paper-search, landscape-synthesis, present-and-ask |
| **direction-narrowing** | Select specific sub-direction | present-candidates + generate-candidate-fields |
| **obstacle-analysis** | Identify and mitigate barriers | identify-obstacles, assess-obstacle-severity, propose-mitigations, ask-obstacle-acceptance |
| **goal-decomposition** | Break goal into actionable sub-goals | formulate-top-goal, and-or-decompose, validate-leaves, feasibility-check, ask-decomposition-validation |
| **north-star-synthesis** | Produce final output artifacts | crystallize-north-star, generate-research-brief, final-validation |

### SOPs by Type (23)

| Type | Count | Execution Model |
|------|-------|-----------------|
| **Dialogue** | 11 | CC talks directly to user — one question at a time, multiple choice preferred |
| **Subagent** | 10 | CC spawns a focused sub-agent with a dedicated prompt.md |
| **Import** | 2 | Delegates to external skill (web-browsing or literature-engine) |

---

## 🎯 Output Artifacts

### 1. North Star Statement

One sentence in the format:

> **"[verb] [specific goal], through [method/path], solving [what problem], ultimately [what impact]"**

Quality criteria: specific (not vague), ambitious (worth a top venue), achievable (within user's capabilities + mitigations).

### 2. Research Brief

Structured context document with 8 sections:

1. North Star — the one-sentence direction
2. Actor Profile — who is doing this research
3. Field Context — selected field + landscape evaluation
4. Chosen Direction — specific sub-direction + rationale
5. Obstacle Landscape — known barriers + mitigations + acceptance
6. Goal Decomposition — GoalTree with priorities
7. Key References — papers and resources discovered during the process
8. Key Terms — vocabulary and concepts central to this research area

The ResearchBrief is a **requirement context document** — it tells downstream strategies WHAT to research and WHY, not HOW.

---

## 🔗 Dependencies

| Dependency | Repository | What It Provides |
|-----------|-----------|-----------------|
| **web-browsing** | [NOESYNTH/web-browsing](https://github.com/NOESYNTH/web-browsing) | `web-search` (quick search) + `web-research` (deep page reading) |
| **literature-engine** | [NOESYNTH/literature-engine](https://github.com/NOESYNTH/literature-engine) | `literature-overview` + `literature-search` + `literature-research` |
| **subagent-spawning** | [NOESYNTH/subagent-spawning](https://github.com/NOESYNTH/subagent-spawning) | Subagent dispatch conventions for 9 subagent SOPs |

### MCP Servers Required

| Server | Purpose |
|--------|---------|
| **brave-search** | Web search API (used by web-browsing skills) |
| **alphaxiv** | Paper search, content extraction, PDF queries (arXiv) |
| **semantic-scholar** | Paper lookup, citations, references, recommendations |

---

## 🚀 Usage

Invoke the `/north-star` skill in a Claude Code session:

```
/north-star-crystallization
```

Or read the entry point directly:

```
Read ENTRY.md. I want to publish a paper but I have no idea what to work on.
```

### Prerequisites

- Claude Code with MCP servers configured (brave-search, alphaxiv, semantic-scholar)
- Sibling repos available: web-browsing, literature-engine, subagent-spawning
- Subagent support enabled (for subagent SOPs to spawn agents)

---

## 📄 License

[Apache-2.0](LICENSE)

---

*A component of the [De-Anthropocentric Research Engine](https://github.com/yogsoth-ai/de-anthropocentric-research-engine), part of the [Yogsoth AI](https://github.com/yogsoth-ai) ecosystem. Built by [Pthahnix](https://github.com/Pthahnix).*
