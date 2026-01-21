# Getting Started with SuperNavigator

Quick guide to installing and using SuperNavigator for the first time.

---

## Installation

### Local Use (Recommended)

```bash
# Use SuperNavigator in your current directory
cd /path/to/SuperNavigator

# Verify structure
ls -la skills/
# Should see: os-layer/ and app-layer/
```

### Plugin Installation (Future)

When available on Claude Code marketplace:
```bash
claude plugin install supernavigator
```

---

## First Project Setup

### 1. Initialize SuperNavigator

In your project directory:
```
"Initialize SuperNavigator in this project"
```

This creates:
- `.agent/` directory structure
- `.nav-config.json` with both layers enabled
- Templates and hooks
- Example documentation

### 2. Verify Installation

Check created structure:
```bash
ls -la .agent/
# Should see: DEVELOPMENT-README.md, .nav-config.json, tasks/, system/, sops/, etc.
```

### 3. Start Your First Session

```
"Start my SuperNavigator session"
```

You should see:
```
╔══════════════════════════════════════════════════════╗
║  🚀 SuperNavigator Session Started                   ║
╚══════════════════════════════════════════════════════╝

⚡ OS Layer (Navigator): Enabled
✨ App Layer (Superpowers): Enabled
🔗 Implicit Integration: Active
```

---

## Your First Workflow

### Design a Feature

```
"Let's design user authentication"
```

- brainstorming skill activates
- nav-marker checkpoint created (automatic)
- Design written to docs/plans/ and .agent/system/

### Create Implementation Plan

```
"Create implementation plan for authentication"
```

- writing-plans skill activates
- Plan written to .agent/tasks/
- nav-task indexes automatically

### Implement with TDD

```
"Set up isolated workspace"
"Implement authentication with TDD"
```

- using-git-worktrees creates branch
- test-driven-development enforces test-first
- Context stays efficient (<50%)

### Code Review

```
"Request code review"
```

- requesting-code-review validates work
- nav-compact auto-triggers if needed (85% threshold)

### Finish

```
"Finish this branch"
```

- finishing-a-development-branch presents options
- nav-marker checkpoint created
- nav-sop suggested for learnings

---

## Key Commands

### Session Management (OS Layer)

```
"Start my SuperNavigator session"        # Begin work
"Create a context marker [name]"         # Save progress
"Clear context and preserve markers"     # Compact after tasks
"Show me session statistics"             # View metrics
```

### Workflows (App Layer)

```
"Let's brainstorm [feature]"              # Design
"Create implementation plan"              # Plan
"Implement with TDD"                      # Develop
"Request code review"                     # Review
"Finish this branch"                      # Complete
```

### Documentation (OS Layer)

```
"Archive TASK-XX documentation"           # After completion
"Create an SOP for debugging [issue]"     # Document solution
```

---

## Configuration

Edit `.agent/.nav-config.json`:

```json
{
  "version": "6.0.0",
  "layers": {
    "os_layer_enabled": true,
    "app_layer_enabled": true
  },
  "tom_features": {
    "verification_checkpoints": true,
    "profile_enabled": true
  },
  "app_layer_features": {
    "tdd_enforced": true,
    "systematic_debugging": true
  },
  "implicit_integration": {
    "auto_save_markers": true,
    "auto_compact_threshold": 0.85,
    "auto_update_nav_tasks": true
  }
}
```

---

## Tips

### Token Efficiency

- Start every session with "Start my SuperNavigator session"
- Let OS layer manage what's loaded
- Don't manually load all docs
- Trust nav-compact to manage context

### Workflow Quality

- Use brainstorming before coding
- Let TDD enforce test-first
- Request code review before merging
- Verify before claiming completion

### Session Continuity

- Create markers before breaks
- Use nav-profile to save preferences
- Let implicit integration handle sync
- Resume from markers after crashes

---

## Next Steps

- [OS Layer Guide](OS-LAYER-GUIDE.md) - Deep dive into Navigator features
- [App Layer Guide](APP-LAYER-GUIDE.md) - Deep dive into Superpowers workflows
- [Implicit Integration](IMPLICIT-INTEGRATION.md) - How layers work together
- [Architecture](../../ARCHITECTURE.md) - System design

---

## Troubleshooting

**"SuperNavigator not initialized"**:
```
Solution: Run "Initialize SuperNavigator in this project"
```

**Skills not activating**:
```
Solution: Check .claude-plugin/plugin.json paths are correct
```

**Context filling up**:
```
Solution: Run "Clear context and preserve markers"
Or: Let nav-compact auto-trigger at 85%
```

**Can't find documentation**:
```
Solution: Run "Start my SuperNavigator session" to load index
```

---

## Support

- Main README: [../../README.md](../../README.md)
- Architecture: [../../ARCHITECTURE.md](../../ARCHITECTURE.md)
- Issues: GitHub (future)
