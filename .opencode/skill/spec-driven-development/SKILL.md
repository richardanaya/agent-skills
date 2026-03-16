---
name: spec-driven-development
description: "Complete workflow for LLM coding agents: initial setup of the template system, adding new features, creating modules/components, using the Constitution as the single integrator, and documenting major architecture changes with ADRs."
license: MIT
compatibility: opencode
metadata:
  category: development-process
  audience: llm-coding-agents
---

# SKILL: Spec-Driven Development with LLM Agents (v2026-03)

## 1. Purpose
You shall use this skill on every coding task, feature request, or architecture discussion.  
It tells you exactly which template to use, how the Constitution integrates everything, when to create modules, and how the entire system tracks what is implemented vs. still pending.

Master this skill and your Local AI Empire stays perfectly clean, instantly knowable, and 100 % under your control.

## 2. Template Hierarchy
1. CONSTITUTION_TEMPLATE.md — single source of truth that integrates every decision  
2. PRODUCT_FEATURE_TEMPLATE.md — any new user-visible capability  
3. COMPONENT_TEMPLATE.md — internal module (only when a feature needs decomposition)  
4. ARCHITECTURE_DECISION_RECORD_TEMPLATE.md — major irreversible change  
5. AGENT_TEMPLATE.md — loaded in every LLM session

## 3. The Convention for Implemented vs Pending Specs
All specs live in these four folders (this is the single source of truth):

```
/specs/
├── features/
│   ├── pending/          ← new or unfinished specs start here
│   └── implemented/      ← moved here when code + tests are complete
└── components/
├── pending/
└── implemented/
```


text- You or an agent creates a spec → put it in the correct `pending/` folder.  
- When the LLM coding agent finishes implementation, its **final action** is:  
> “git mv this file from pending/ to implemented/”  
(and include the move in the same commit as the code).

This folder method requires zero extra text inside files and lets you (or any agent) know the status of the entire empire at a glance.

## 4. When to Use Each Template

### Initial Setup (do this once)
- Create the `/specs/` folder structure above.  
- Write the first **CONSTITUTION** (this becomes the integrator for the whole empire).  
- Load the **AGENT_TEMPLATE** into your main LLM coding agent.

### Adding New Features
- Create a file from **PRODUCT_FEATURE_TEMPLATE.md** and place it in `/specs/features/pending/`.  
- This is for anything the user will see or interact with.

### Creating Modules / Components
- Only when one feature spec feels too large (>50 requirements or multiple internal concerns).  
- Create files from **COMPONENT_TEMPLATE.md** in `/specs/components/pending/`.  
- Each component gets its own tight Purpose + Functional Requirements + Verification Criteria.

### Documenting Major Architecture Changes
- Any time you make an irreversible or high-impact decision (new format, performance trade-off, new dependency, security boundary, etc.).  
- Immediately create an **ARCHITECTURE_DECISION_RECORD_TEMPLATE.md** in `/specs/` (or a subfolder) and link it from the relevant feature or component spec.

### Why the Constitution is Required
It is the single document that prevents every feature and module from repeating the same rules (WebAssembly-only, <50 ms, zero cloud, etc.).  
Reference it with one line in every spec. Without it, the system would bloat and drift.

## 5. Exact Workflow (follow every time)
1. Confirm Constitution exists (the integrator).  
2. Decide which template is needed using section 4 above.  
3. If no spec exists, create it in the correct `pending/` folder.  
4. Once a completed spec is attached to an agent:  
- Short Implementation Plan  
- Implement ONLY what is specified  
- Full code files + tests for every Verification Criteria  
- Compliance Checklist (maps back to spec + Constitution)  
- Final step: git mv the spec to the `implemented/` folder  
5. Commit everything together.

## 6. Forbidden Actions
- Skip the Constitution reference  
- Add anything not in the spec  
- Make major architecture changes without an ADR  
- Leave specs in pending/ after they are implemented  
- Use any other status-tracking method (no frontmatter, no tags, no spreadsheets)

Master this skill and every new feature, module, or change will slot into your empire instantly — giving you back hours every week for strength training, family dinners, shakuhachi practice, Korean sauce mastery, Japan trip planning, and everything else that matters.

You now possess the complete Spec-Driven Development skill.