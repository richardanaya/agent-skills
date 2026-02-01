---
name: bd-create-new-product
description: Create a new product with a structured chain of related issues using the bd (beads) issue tracker - sets up epics, tasks, and dependencies for product development
---

## What I Do
- Create a new product epic as the parent container
- Generate a chain of related issues for product development phases
- Set up proper dependencies between issues (research → design → development → testing → launch)
- Create milestone markers for tracking progress
- Establish a structured workflow for the product lifecycle

## When to Use Me
Use this skill when you need to:
- Kick off a new product initiative
- Set up a structured project with clear phases
- Create a product roadmap with dependent tasks
- Establish a complete development workflow
- Onboard a new product with proper issue tracking

## bd Commands to Use

### Initialize Product Epic
```
bd epic create --title "<Product Name>" --description "<product vision and scope>"
```
Creates the parent epic that will contain all related issues.

### Create Issue Chain
```
bd create --title "Research & Discovery" --type task --description "<research requirements>" -p <epic-id>
bd create --title "Requirements Definition" --type task --description "<requirements>" -p <epic-id>
bd create --title "Design & Architecture" --type task --description "<design scope>" -p <epic-id>
bd create --title "Implementation" --type task --description "<development work>" -p <epic-id>
bd create --title "Testing & QA" --type task --description "<testing scope>" -p <epic-id>
bd create --title "Documentation" --type task --description "<docs needed>" -p <epic-id>
bd create --title "Launch & Deploy" --type task --description "<deployment steps>" -p <epic-id>
```
Creates the core development chain under the epic.

### Chain Dependencies
```
bd dep add <requirements-id> <research-id>
bd dep add <design-id> <requirements-id>
bd dep add <implementation-id> <design-id>
bd dep add <testing-id> <implementation-id>
bd dep add <docs-id> <implementation-id>
bd dep add <launch-id> <testing-id>
bd dep add <launch-id> <docs-id>
```
Links issues in a sequential dependency chain.

### Set Issue Types and Labels
```
bd label add <issue-id> phase-1
bd label add <issue-id> milestone
bd label add <issue-id> critical-path
```
Tags issues for filtering and organization.

### View Product Structure
```
bd epic show <epic-id>
bd graph
bd dep list <issue-id>
```
Shows the product structure and dependencies.

### Check Ready Work
```
bd ready
```
Shows what issues are ready to work on (no blockers).

## Workflow for Creating New Product

1. **Create the Epic**: Use `bd epic create` to establish the product container
2. **Create Issues**: Use `bd create` with `-p <epic-id>` to create child issues
3. **Chain Dependencies**: Use `bd dep add` to link issues in order
4. **Add Labels**: Use `bd label add` for categorization and filtering
5. **Verify Structure**: Use `bd graph` and `bd epic show` to confirm setup

## Typical Product Issue Chain

```
Epic: Product X Development
├── Task: Research & Discovery (OPEN)
│   └── Dep: None (ready to start)
├── Task: Requirements Definition (OPEN)
│   └── Dep: Research & Discovery
├── Task: Design & Architecture (OPEN)
│   └── Dep: Requirements Definition
├── Task: Implementation (OPEN)
│   └── Dep: Design & Architecture
├── Task: Testing & QA (OPEN)
│   └── Dep: Implementation
├── Task: Documentation (OPEN)
│   └── Dep: Implementation
└── Task: Launch & Deploy (OPEN)
    └── Dep: Testing & QA, Documentation
```

## Best Practices

- **Start with Research**: Always begin with discovery before committing to solutions
- **Sequential Dependencies**: Link issues so work flows naturally from one phase to the next
- **Parallel Work**: Identify which tasks can run in parallel (e.g., docs with testing)
- **Critical Path**: Label the main development line for priority focus
- **Milestone Labels**: Use labels to mark major checkpoints
- **Keep It Lean**: Don't over-engineer the chain - focus on real dependencies

## Quick Command Reference

**Check what's ready to work on:**
```
bd ready
```

**View dependency graph:**
```
bd graph
```

**See blocked issues:**
```
bd blocked
```

**List all issues in epic:**
```
bd epic show <epic-id>
```

**Show product status:**
```
bd status
```
