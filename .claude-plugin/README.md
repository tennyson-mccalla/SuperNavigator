# SuperNavigator Plugin

Unified OS + Application Layer for Claude Code Development.

## Installation

### Local Installation

1. **Install as Claude Code plugin**:
```bash
claude plugin install https://github.com/dkyazzentwatwa/SuperNavigator
```

2. **Restart Claude Code**

3. **Verify installation** - In Claude Code, say:
```
"List available skills"
```

You should see SuperNavigator skills (nav-init, brainstorming, test-driven-development, etc.)

## Quick Start

### 1. Initialize SuperNavigator

```
"Initialize SuperNavigator in this project"
```

This creates:
- `.agent/` directory structure
- `.nav-config.json` with both layer settings
- Templates and hooks

### 2. Start Your Session

```
"Start my SuperNavigator session"
```

This loads:
- OS layer context (DEVELOPMENT-README.md)
- App layer workflows (using-superpowers)
- Both layers active and integrated

### 3. Use Skills Naturally

**OS Layer** (Navigator):
- "Create a context marker for authentication feature"
- "Show me session statistics"
- "Compact the context"

**App Layer** (Superpowers):
- "Let's brainstorm a new feature"
- "Create implementation plan"
- "Set up TDD workflow"
- "Request code review"

## Plugin Structure

```
supernavigator/
├── .claude-plugin/
│   ├── plugin.json          # Plugin manifest (31 skills)
│   ├── marketplace.json     # Marketplace metadata
│   └── README.md            # This file
│
├── skills/
│   ├── os-layer/            # 17 Navigator skills
│   └── app-layer/           # 14 Superpowers skills
│
├── templates/               # Project templates
├── .agent/                  # Example structure
└── README.md                # Main documentation
```

## What's Inside

### OS Layer (17 Skills)
- **Core**: nav-init, nav-start, nav-onboard, nav-loop
- **Context/Memory**: nav-profile, nav-marker, nav-compact, nav-diagnose
- **Documentation**: nav-task, nav-sop, nav-skill-creator
- **Project Management**: nav-stats, nav-update-claude, nav-release, nav-upgrade, nav-install-multi-claude
- **Plugin**: plugin-slash-command

### App Layer (14 Skills)
- **Design**: brainstorming, writing-plans
- **Development**: test-driven-development, using-git-worktrees, executing-plans
- **Quality**: requesting-code-review, receiving-code-review, systematic-debugging
- **Parallel**: dispatching-parallel-agents, subagent-driven-development
- **Advanced**: verification-before-completion, finishing-a-development-branch, writing-skills, using-superpowers

## Features

### From Navigator (OS Layer)
- 92% token reduction via on-demand loading
- Theory of Mind integration (verification checkpoints, bilateral modeling)
- Loop Mode with structured completion
- Session statistics and metrics

### From Superpowers (App Layer)
- Test-Driven Development enforcement
- Systematic debugging processes
- Code review patterns
- Parallel development with subagents

### Integration
- Implicit triggers at workflow boundaries
- Auto-save markers during brainstorming, code review
- Auto-compact at 85% context usage
- Shared `.agent/` data store

## Configuration

After initialization, configure in `.agent/.nav-config.json`:

```json
{
  "version": "6.0.0",
  "layers": {
    "os_layer_enabled": true,
    "app_layer_enabled": true
  },
  "tom_features": {
    "verification_checkpoints": true,
    "profile_enabled": true,
    "diagnose_enabled": true
  },
  "app_layer_features": {
    "tdd_enforced": true,
    "git_worktrees_enabled": true,
    "systematic_debugging": true
  },
  "implicit_integration": {
    "auto_save_markers": true,
    "auto_compact_threshold": 0.85,
    "auto_update_nav_tasks": true
  }
}
```

## Documentation

- [Main README](../README.md) - Architecture and philosophy
- [ARCHITECTURE.md](../ARCHITECTURE.md) - Layered system deep dive
- [Getting Started Guide](../docs/guides/GETTING-STARTED.md)
- [OS Layer Guide](../docs/guides/OS-LAYER-GUIDE.md)
- [App Layer Guide](../docs/guides/APP-LAYER-GUIDE.md)

## Support

- Issues: https://github.com/dkyazzentwatwa/SuperNavigator/issues
- Discussions: https://github.com/dkyazzentwatwa/SuperNavigator/discussions

## License

MIT - See [LICENSE](../LICENSE)

## Credits

Built on the shoulders of:
- **Navigator** by Aleks Petrov - https://github.com/alekspetrov/navigator
- **Superpowers** by Jesse Vincent - https://github.com/obra/superpowers

Unified and extended for Claude Code.
