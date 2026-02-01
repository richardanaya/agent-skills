---
name: bd-modify-product-description-and-tasks
description: Modify product descriptions and tasks using the bd (beads) issue tracker - create, edit, update, and manage issues with proper dependency handling
---

## What I Do
- Create new issues with proper descriptions and metadata
- Edit existing issue descriptions and fields
- Update issue states and progress
- Manage issue dependencies and relationships
- Label and categorize issues appropriately
- Add comments and context to issues
- Move issues between rigs/projects when needed

## When to Use Me
Use this skill when you need to:
- Create a new task or issue with full context
- Update an existing issue's description or details
- Change an issue's state (open, in-progress, closed, etc.)
- Add or modify dependencies between issues
- Label issues for better organization
- Add comments to provide updates or context
- Split or reorganize work items

## bd Commands to Use

### Create a New Issue
```
bd create --title "<title>" --type <type> [--description "<description>"]
```
Creates a new issue. Common types: task, bug, feature, epic

### Create from Markdown File
```
bd create --file <path-to-markdown>
```
Creates issues from a markdown file (useful for bulk creation).

### Interactive Create
```
bd create-form
```
Creates an issue using an interactive form in your $EDITOR.

### Quick Capture
```
bd q --title "<title>"
```
Quickly create an issue and output only the ID (useful for scripts).

### Edit an Issue
```
bd edit <issue-id>
```
Opens the issue in $EDITOR to modify fields.

### Update Specific Fields
```
bd update <issue-id> --title "<new-title>"
bd update <issue-id> --description "<new-description>"
bd update <issue-id> --type <new-type>
```
Update individual fields without opening an editor.

### Set State
```
bd set-state <issue-id> <state>
```
Set operational state (creates event + updates label). States: open, in_progress, closed, etc.

### Close/Reopen Issues
```
bd close <issue-id> [<issue-id>...]
bd reopen <issue-id> [<issue-id>...]
```

### Manage Dependencies
```
bd dep add <issue-id> <depends-on-issue-id>
bd dep remove <issue-id> <depends-on-issue-id>
bd dep list <issue-id>
```

### Add Labels
```
bd label add <issue-id> <label>
bd label remove <issue-id> <label>
```

### Add Comments
```
bd comments add <issue-id> "<comment-text>"
```

### View Issue Details
```
bd show <issue-id>
```
Show full issue details including description, state, dependencies, comments.

### Move Issues Between Rigs
```
bd move <issue-id> <target-rig>
```
Move an issue to a different rig with automatic dependency remapping.

### Mark as Duplicate
```
bd duplicate <issue-id> <original-issue-id>
```

### Supersede an Issue
```
bd supersede <old-issue-id> <new-issue-id>
```
Mark an issue as superseded by a newer one.

## Workflow for Creating Issues

1. **Define the work**: Determine title, type, and description
2. **Create the issue**: Use `bd create` or `bd create-form`
3. **Set dependencies**: Use `bd dep add` to establish relationships
4. **Add labels**: Use `bd label add` for categorization
5. **Verify**: Use `bd show` to confirm everything is correct

## Workflow for Modifying Issues

1. **View current state**: Use `bd show <issue-id>` to see existing details
2. **Make changes**: Use `bd edit` for complex changes or `bd update` for simple field updates
3. **Update state**: Use `bd set-state` when work progresses
4. **Add context**: Use `bd comments add` to document decisions or progress
5. **Sync**: Changes auto-sync to JSONL (or run `bd sync` if needed)

## Best Practices

- **Clear titles**: Make issue titles descriptive and actionable
- **Detailed descriptions**: Include context, acceptance criteria, and links
- **Dependencies**: Always set up dependencies before starting work
- **State updates**: Keep issue state current as work progresses
- **Comments**: Add comments for significant decisions or blockers
- **Labels**: Use consistent labeling for easy filtering
