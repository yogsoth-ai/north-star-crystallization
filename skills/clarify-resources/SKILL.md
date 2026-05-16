---
name: clarify-resources
description: Understand what resources the user has available for research — compute, timeline, collaboration, data access, experimental environment. Every item accepts '待定' as a valid answer.
execution: dialogue
---

# Clarify Resources

Map the user's available resources.

## Execution

Dialogue — inline, no subagent.

## What to Ask About (one at a time)

- Compute: local GPU specs / cloud budget / CPU-only
- Timeline: hard deadline? flexible? how many months?
- Collaboration: solo / advisor / team / cross-institution
- Data access: public datasets? proprietary? need to collect?
- Experimental environment: dry-lab only? wet-lab access?

## Key Behavior

Every item accepts "待定" (TBD) as a valid answer. Note TBD items — they may need revisiting later.

## Output

Resources section of ActorProfile.
