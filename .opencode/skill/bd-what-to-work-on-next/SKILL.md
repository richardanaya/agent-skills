---
name: bd-what-to-work-on-next
description: Determine what to work on next using the bd (beads) issue tracker by analyzing open issues, dependencies, and ready work
---

## What I Do
- Analyze the current state of issues using bd commands
- Identify what work is ready (no blockers, open or in-progress)
- Show blocked issues that need attention
- List stale issues that haven't been updated recently
- Present the issue dependency graph to understand relationships
- Display priority issues based on dependencies and state

## When to Use Me
Use this skill when you need to:
- Start a new work session and need to prioritize
- Check what's currently ready to work on
- Identify blockers and dependencies that need resolution
- Review stale issues that may need attention
- Understand the overall project status before planning

## Git + JSONL: How bd Works

**No database servers. No cloud APIs. Just Git + JSONL.**

All issues live in `.beads/issues.jsonl` — a simple JSON Lines file that git tracks like any other code. This means:

- **Pull → see updates**: `git pull` brings down everyone's issue changes
- **Push → share yours**: `git push` publishes your issue updates to the team
- **Merge conflicts are possible**: If two people edit the same issue simultaneously, you'll get a classic git merge conflict (just like with code)
- **Hash IDs reduce conflicts**: Every issue has a unique hash ID, making simultaneous edits on *different* issues seamless

This is version control for your project management — fully distributed, offline-capable, and conflict-aware.

## bd Commands to Use

### Check Ready Work (No Blockers)
```
bd ready
```
Shows all issues that are ready to work on - no blockers, in open or in-progress state.

### Check Blocked Issues
```
bd blocked
```
Lists all issues that are currently blocked by dependencies.

### List Open Issues
```
bd list --state open
```
Shows all open issues with basic details.

### Check Dependencies
```
bd dep list <issue-id>
```
Shows what a specific issue depends on or what depends on it.

### View Dependency Graph
```
bd graph
```
Displays a visual graph of issue dependencies to understand relationships.

### Check Stale Issues
```
bd stale
```
Shows issues that haven't been updated recently and may need attention.

### Check Overall Status
```
bd status
```
Shows issue database overview and statistics.

### Activity Feed
```
bd activity
```
Shows real-time molecule state feed of recent changes.

### View Epic Structure
```
bd epic list
```
Lists all epics to see high-level work streams.

### Search for Specific Issues
```
bd search "<query>"
```
Search for issues by text query when looking for something specific.

## Workflow

1. **Start with overview**: Run `bd status` and `bd ready` to understand current state
2. **Identify blockers**: Run `bd blocked` to see what's stuck
3. **Check context**: Run `bd graph` to visualize dependencies
4. **Review stale items**: Run `bd stale` to find neglected issues
5. **Prioritize**: Based on the data, recommend the highest priority issue to work on next

## Decision Framework

When recommending what to work on next, consider:
- Issues in `ready` state are immediate candidates
- Blocked issues may need dependency resolution first
- Stale issues might indicate forgotten work
- Issues with many dependents should be prioritized (unblock others)
- Consider the user's role and expertise when making recommendations
