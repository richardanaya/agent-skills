---
name: bd-create-new-product
description: Create a new product with a structured chain of related issues using the bd (beads) issue tracker - sets up epics, tasks, and dependencies for product development
---

## What I Do
- Initialize git repository and configure bd properly
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

## Git + JSONL: How bd Works

**No database servers. No cloud APIs. Just Git + JSONL.**

All issues live in `.beads/issues.jsonl` — a simple JSON Lines file that git tracks like any other code. This means:

- **Pull → see updates**: `git pull` brings down everyone's issue changes
- **Push → share yours**: `git push` publishes your issue updates to the team
- **Merge conflicts are possible**: If two people edit the same issue simultaneously, you'll get a classic git merge conflict (just like with code)
- **Hash IDs reduce conflicts**: Every issue has a unique hash ID, making simultaneous edits on *different* issues seamless

This is version control for your project management — fully distributed, offline-capable, and conflict-aware.

## bd Commands to Use

### Initialize Repository and Setup
```bash
# Step 1: Initialize git repository first (required for bd)
git init
# Step 2: Initialize bd with a project prefix
bd init --prefix <project-name>
# Step 3: Enable no-db mode (CRITICAL - makes JSONL the source of truth)
# Edit .beads/config.yaml and set: no-db: true
# Step 4: If you see "LEGACY DATABASE" warnings, migrate the repo ID
bd migrate --update-repo-id
```

**CRITICAL: Enable no-db mode in `.beads/config.yaml`**

Edit `.beads/config.yaml` and add:
```yaml
# Use no-db mode: load from JSONL, no SQLite, write back after each command
# When true, bd will use .beads/issues.jsonl as the source of truth
# instead of SQLite database
no-db: true
```

This makes **`.beads/issues.jsonl` the source of truth** — every bd command reads from and writes directly to the JSONL file. No SQLite database. Full git tracking of every issue change.

**Verify: Your `.beads/` folder should only contain 3 files:**
```bash
$ ls -la .beads/
config.yaml       # Your configuration with no-db: true
issues.jsonl      # All issues stored as JSON Lines (git-tracked)
metadata.json     # Project metadata (prefix, repo binding, etc.)
```

**No `beads.db` file!** If you see a `.beads/beads.db` file, you haven't enabled no-db mode correctly. SQLite database files should not exist — all data lives in JSONL.

**Important**: Always run `git init` before `bd init` to avoid repository ID warnings. If warnings persist after creation, run `bd migrate --update-repo-id`.

### Initialize Product Epic
```
bd create "<Product Name>" --type epic --description "<product vision and scope>"
```
Creates the parent epic that will contain all related issues.

### Create Issue Chain
```
bd create "Research & Discovery" --type task --description "<research requirements>" -p <epic-id>
bd create "Project Setup & Dependencies" --type task --description "<setup requirements>" -p <epic-id>
bd create "Design & Architecture" --type task --description "<design scope>" -p <epic-id>
bd create "Core Implementation" --type task --description "<development work>" -p <epic-id>
bd create "Testing & QA" --type task --description "<testing scope>" -p <epic-id>
bd create "Documentation" --type task --description "<docs needed>" -p <epic-id>
bd create "Release & Deploy" --type task --description "<deployment steps>" -p <epic-id>
```
Creates the core development chain under the epic.

### Chain Dependencies
```
bd dep add <setup-id> <research-id>
bd dep add <design-id> <research-id>
bd dep add <implementation-id> <design-id>
bd dep add <testing-id> <implementation-id>
bd dep add <docs-id> <implementation-id>
bd dep add <release-id> <testing-id>
bd dep add <release-id> <docs-id>
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
cat .beads/beads.jsonl | head -20
```
Shows the product structure and dependencies.

### Check Ready Work
```
bd ready
```
Shows what issues are ready to work on (no blockers).

## Complete Workflow for Creating New Product

1. **Initialize Git**: Run `git init` to create a git repository
2. **Initialize bd**: Run `bd init --prefix <name>` to set up the database
3. **Enable no-db mode**: Edit `.beads/config.yaml` and set `no-db: true` — this makes JSONL the source of truth
4. **Fix Warnings**: If you see "LEGACY DATABASE" warnings, run `bd migrate --update-repo-id`
5. **Create the Epic**: Use `bd create` with `--type epic` to establish the product container
6. **Create Issues**: Use `bd create` with `-p <epic-id>` to create child issues
7. **Chain Dependencies**: Use `bd dep add` to link issues in order
8. **Add Labels**: Use `bd label add` for categorization and filtering
9. **Verify Structure**: Use `bd status` to confirm everything is set up correctly
10. **Verify no-db mode**: Check that `.beads/` only contains `config.yaml`, `issues.jsonl`, and `metadata.json` (no `beads.db`!)

## Typical Product Issue Chain

```
Epic: Product X Development
├── Task: Research & Discovery [OPEN]
│   └── Ready to start (no dependencies)
├── Task: Project Setup & Dependencies [OPEN]
│   └── Can run parallel with Research
├── Task: Design & Architecture [OPEN]
│   └── Dep: Research & Discovery
├── Task: Core Implementation [OPEN]
│   └── Dep: Project Setup, Design & Architecture
├── Task: Testing & QA [OPEN]
│   └── Dep: Core Implementation
├── Task: Documentation [OPEN]
│   └── Dep: Core Implementation
└── Task: Release & Deploy [OPEN]
    └── Dep: Testing & QA, Documentation
```

## Best Practices

- **Git First**: Always initialize git before bd to avoid repository ID warnings
- **Fix Warnings Early**: Run `bd migrate --update-repo-id` if you see legacy database warnings
- **Start with Research**: Always begin with discovery before committing to solutions
- **Sequential Dependencies**: Link issues so work flows naturally from one phase to the next
- **Parallel Work**: Identify which tasks can run in parallel (e.g., setup with research, docs with testing)
- **Critical Path**: Label the main development line for priority focus
- **Milestone Labels**: Use labels to mark major checkpoints
- **Keep It Lean**: Don't over-engineer the chain - focus on real dependencies

## Troubleshooting

### "LEGACY DATABASE DETECTED" Warning
If you see this warning:
```
bd migrate --update-repo-id
```
This binds the database to your git repository and prevents the warnings.

### Repository Not Initialized
If bd shows "No git repository initialized":
```
git init
bd migrate --update-repo-id
```

## Quick Command Reference

**Initialize properly:**
```bash
git init
bd init --prefix my-project
# CRITICAL: Edit .beads/config.yaml and set no-db: true
echo "no-db: true" >> .beads/config.yaml
bd migrate --update-repo-id  # If needed
# Verify: Should only see config.yaml, issues.jsonl, metadata.json
ls -la .beads/
```

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
