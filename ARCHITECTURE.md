# SuperNavigator Architecture

**Layered System Design: OS Layer + Application Layer**

---

## Table of Contents

1. [Overview](#overview)
2. [Layered Architecture](#layered-architecture)
3. [OS Layer (Navigator)](#os-layer-navigator)
4. [Application Layer (Superpowers)](#application-layer-superpowers)
5. [Communication Layer (.agent/)](#communication-layer-agent)
6. [Implicit Integration](#implicit-integration)
7. [Data Flow](#data-flow)
8. [Design Decisions](#design-decisions)

---

## Overview

SuperNavigator uses a **layered architecture** to separate concerns:

- **OS Layer**: Manages WHEN and WHAT to load (context management)
- **App Layer**: Defines HOW to develop (workflows and patterns)
- **Communication**: Shared `.agent/` data store with implicit triggers

This separation enables:
- Specialization (each layer does one thing well)
- Loose coupling (layers work independently)
- Tight integration (implicit triggers connect workflows)

---

## Layered Architecture

### Visual Representation

```
┌──────────────────────────────────────────────────────┐
│               USER INTERACTION                       │
│    Natural Language → Skill Invocation               │
└──────────────────────────────────────────────────────┘
                        ↓
┌──────────────────────────────────────────────────────┐
│         APPLICATION LAYER (Superpowers)              │
│                                                      │
│  ┌────────────┐  ┌──────────────┐  ┌──────────────┐│
│  │  Design    │  │ Development  │  │   Quality    ││
│  │            │  │              │  │              ││
│  │ brainstorm │  │     TDD      │  │ code-review  ││
│  │ write-plan │  │ worktrees    │  │  debugging   ││
│  └────────────┘  └──────────────┘  └──────────────┘│
│                                                      │
│  Writes to: .agent/tasks/, .agent/system/           │
└──────────────────────────────────────────────────────┘
                        ↕
            ┌─────────────────────┐
            │  .agent/ Data Store │ ← INTEGRATION
            │  (Shared Storage)   │
            └─────────────────────┘
                        ↕
┌──────────────────────────────────────────────────────┐
│            OS LAYER (Navigator)                      │
│                                                      │
│  ┌────────────┐  ┌──────────────┐  ┌──────────────┐│
│  │  Session   │  │   Context    │  │    Memory    ││
│  │            │  │              │  │              ││
│  │ nav-init   │  │ nav-compact  │  │  nav-marker  ││
│  │ nav-start  │  │ nav-diagnose │  │  nav-profile ││
│  └────────────┘  └──────────────┘  └──────────────┘│
│                                                      │
│  Reads from: .agent/DEVELOPMENT-README.md            │
│  Indexes: .agent/tasks/, .agent/system/             │
└──────────────────────────────────────────────────────┘
```

### Layer Responsibilities

| Aspect | OS Layer | App Layer |
|--------|----------|-----------|
| **Primary Concern** | Context efficiency | Development quality |
| **When Active** | Every session | On-demand workflows |
| **State Management** | Persistent (.agent/) | Transient (per-workflow) |
| **User Interaction** | Session start/end | Throughout development |
| **Integration** | Reads .agent/, creates markers | Writes to .agent/ |

---

## OS Layer (Navigator)

### Purpose

Manage context loading, session state, and memory to keep token usage efficient.

### Core Skills (17)

**Session Management**:
- `nav-init`: Initialize .agent/ structure
- `nav-start`: Load documentation navigator
- `nav-onboard`: User onboarding
- `nav-loop`: Autonomous task completion

**Context Optimization**:
- `nav-compact`: Prune context intelligently
- `nav-marker`: Create restoration checkpoints
- `nav-profile`: Theory of Mind (user preferences)
- `nav-diagnose`: Detect collaboration quality issues

**Documentation**:
- `nav-task`: Index implementation plans
- `nav-sop`: Standard Operating Procedures
- `nav-skill-creator`: Create new skills

**Project Management**:
- `nav-stats`: Session metrics
- `nav-update-claude`: Update CLAUDE.md
- `nav-release`: Release management
- `nav-upgrade`: Version upgrades
- `nav-install-multi-claude`: Multi-Claude workflows

**Plugin**:
- `plugin-slash-command`: Slash command support

### Key Features

**92% Token Reduction**:
```
Without Navigator: Load entire .agent/ = 150k tokens
With Navigator:    Load DEVELOPMENT-README.md = 12k tokens
                   Load on-demand = 3-5k per doc
                   Total = ~20k vs 150k (87% savings)
```

**Theory of Mind** (v5.0.0+):
- Bilateral modeling (nav-profile)
- Verification checkpoints
- Quality detection (nav-diagnose)
- Belief state anchors

**Loop Mode** (v5.1.0+):
- Structured completion signals
- Dual-condition exit gates
- Stagnation detection
- Autonomous task execution

### Data Sources

**Reads**:
- `.agent/DEVELOPMENT-README.md` (navigation index)
- `.agent/.nav-config.json` (configuration)
- `.agent/markers/*.md` (checkpoints)
- `.agent/profiles/*.json` (user preferences)

**Writes**:
- `.agent/markers/` (new checkpoints)
- `.agent/profiles/` (updated preferences)
- Updates to DEVELOPMENT-README.md

---

## Application Layer (Superpowers)

### Purpose

Provide structured development workflows from design to deployment.

### Core Skills (14)

**Design**:
- `brainstorming`: Turn ideas into designs
- `writing-plans`: Create implementation plans

**Development**:
- `test-driven-development`: RED-GREEN-REFACTOR
- `using-git-worktrees`: Isolated workspaces
- `executing-plans`: Task-by-task execution

**Quality**:
- `requesting-code-review`: Validate work
- `receiving-code-review`: Process feedback
- `systematic-debugging`: Root-cause analysis

**Parallel**:
- `dispatching-parallel-agents`: Independent tasks
- `subagent-driven-development`: Complex features

**Advanced**:
- `verification-before-completion`: Ensure it works
- `finishing-a-development-branch`: Merge/PR decisions
- `writing-skills`: Create new skills
- `using-superpowers`: Skill usage guide

### Key Principles

**Test-Driven Development**:
- Write failing test first
- Minimal code to pass
- Refactor with confidence
- 100% enforcement

**Systematic Over Ad-Hoc**:
- Brainstorming before coding
- Plans before implementation
- Debugging process before fixes
- Verification before completion

**Simplicity**:
- YAGNI ruthlessly
- No premature abstraction
- Solve the problem at hand
- Refactor when needed

### Data Sources

**Reads**:
- Git repository state
- Test results
- Code review comments
- Plan files

**Writes**:
- `docs/plans/YYYY-MM-DD-*.md` (designs)
- `.agent/tasks/TASK-*.md` (plans)
- `.agent/sops/` (procedures)
- `.agent/system/` (architecture updates)

---

## Communication Layer (.agent/)

### Directory Structure

```
.agent/
├── DEVELOPMENT-README.md      # OS layer navigation index
├── .nav-config.json           # Configuration (both layers)
│
├── tasks/                     # App layer writes
│   └── TASK-XX-feature.md     # writing-plans output
│
├── system/                    # App layer writes
│   ├── project-architecture.md
│   └── patterns.md            # brainstorming output
│
├── sops/                      # App layer writes
│   ├── integrations/
│   ├── debugging/             # systematic-debugging output
│   ├── development/
│   └── deployment/
│
├── markers/                   # OS layer writes
│   └── checkpoint-*.md        # nav-marker output
│
├── profiles/                  # OS layer writes
│   └── user-preferences.json  # nav-profile output
│
└── grafana/                   # OS layer metrics
    └── navigator-dashboard.json
```

### Data Flow

**App Layer → OS Layer**:
```
brainstorming writes design
  ↓
.agent/system/architecture.md
  ↓
nav-task indexes in DEVELOPMENT-README.md
  ↓
nav-start loads index next session
```

**OS Layer → App Layer**:
```
nav-marker creates checkpoint
  ↓
.agent/markers/before-brainstorming.md
  ↓
If session crashes, nav-start offers restore
  ↓
App layer continues from checkpoint
```

---

## Implicit Integration

### Trigger Boundaries

Defined in `.nav-config.json`:

```json
{
  "implicit_integration": {
    "trigger_boundaries": [
      "before_brainstorming",
      "after_plan_complete",
      "after_code_review",
      "on_branch_finish"
    ]
  }
}
```

### Integration Points

**1. Before Brainstorming**:
```
User: "Let's design authentication"
  ↓
App Layer: brainstorming skill activates
  ↓
OS Layer: nav-marker creates checkpoint
  ↓
Checkpoint: .agent/markers/before-brainstorm-auth.md
```

**2. After Plan Complete**:
```
App Layer: writing-plans creates plan
  ↓
Plan written to: .agent/tasks/TASK-12-auth.md
  ↓
OS Layer: nav-task updates index
  ↓
Index updated: .agent/DEVELOPMENT-README.md
```

**3. After Code Review**:
```
App Layer: requesting-code-review completes
  ↓
OS Layer: Check context usage
  ↓
If > 85%: nav-compact auto-triggers
```

**4. On Branch Finish**:
```
App Layer: finishing-a-development-branch
  ↓
OS Layer: nav-marker creates completion checkpoint
  ↓
OS Layer: nav-sop suggests documenting learnings
```

### Configuration

Enable/disable implicit integration:

```json
{
  "implicit_integration": {
    "auto_save_markers": true,        // Markers at boundaries
    "auto_compact_threshold": 0.85,   // Compact at 85%
    "auto_update_nav_tasks": true,    // Index plans
    "trigger_boundaries": [...]       // When to trigger
  }
}
```

---

## Data Flow

### Session Start Flow

```
1. User: "Start my SuperNavigator session"
   ↓
2. nav-start (OS layer) executes
   ↓
3. Loads: .agent/DEVELOPMENT-README.md (2k tokens)
   ↓
4. Loads: .agent/.nav-config.json (config)
   ↓
5. Checks: .agent/profiles/user.json (preferences)
   ↓
6. Injects: using-superpowers context (App layer)
   ↓
7. Both layers active
```

### Workflow Execution Flow

```
1. User: "Design new feature"
   ↓
2. brainstorming (App) activates
   ↓
3. nav-marker (OS) checkpoint created (implicit)
   ↓
4. Design written to docs/plans/ and .agent/system/
   ↓
5. nav-task (OS) indexes design (implicit)
   ↓
6. Design accessible in future sessions
```

### Context Management Flow

```
1. App layer workflow runs
   ↓
2. Context usage grows
   ↓
3. Reaches 85% threshold
   ↓
4. nav-compact (OS) auto-triggers (implicit)
   ↓
5. Context pruned intelligently
   ↓
6. Workflow continues with <50% usage
```

---

## Design Decisions

### Why Layered Architecture?

**Separation of Concerns**:
- OS layer: Optimization (when/what to load)
- App layer: Execution (how to develop)
- Clean boundaries, independent evolution

**Loose Coupling**:
- Layers communicate via `.agent/` files
- No direct skill-to-skill dependencies
- Easy to add/remove skills

**Tight Integration**:
- Implicit triggers connect workflows
- No manual coordination needed
- Seamless user experience

### Why Shared .agent/?

**Single Source of Truth**:
- Both layers read/write same structure
- No data synchronization needed
- Consistent state

**Observable**:
- User can inspect .agent/ anytime
- Easy to debug integration issues
- Transparent operation

**Simple**:
- No complex event bus
- No message passing
- Just files

### Why Implicit Integration?

**Better UX**:
- No manual trigger commands
- Workflows feel natural
- Reduced cognitive load

**Reliable**:
- Triggers at consistent boundaries
- No user error possible
- Always synchronized

**Optional**:
- Can be disabled in config
- Explicit mode available
- User control maintained

---

## Performance Characteristics

### Token Usage

**Session Start**:
```
OS Layer loads:
- DEVELOPMENT-README.md: 2k tokens
- .nav-config.json: 0.5k tokens
- using-superpowers: 3k tokens
Total: ~5.5k tokens
```

**Typical Workflow**:
```
Design phase:
- brainstorming dialogue: 10k tokens
- Design doc: 3k tokens

Implementation phase:
- test-driven-development: 5k tokens
- Code context: 20k tokens

Review phase:
- requesting-code-review: 8k tokens

Total: ~46k tokens (vs 150k without Navigator)
```

### Session Length

**Without SuperNavigator**:
- Crashes at exchange 5-7
- Context fills completely
- Must restart frequently

**With SuperNavigator**:
- 20+ exchanges common
- Context stays <50%
- Markers enable resume
- Sessions complete features

---

## Extension Points

### Adding OS Layer Skills

1. Create skill in `skills/os-layer/{category}/`
2. Add to `.claude-plugin/plugin.json`
3. Document in OS-LAYER-GUIDE.md
4. Test with nav-start

### Adding App Layer Skills

1. Create skill in `skills/app-layer/{category}/`
2. Add to `.claude-plugin/plugin.json`
3. Add SuperNavigator integration section
4. Document integration points
5. Test workflow with OS layer

### Adding Integration Points

1. Update `.nav-config.json` template
2. Add trigger boundary to `trigger_boundaries`
3. Update skill documentation
4. Test implicit trigger behavior

---

## Migration Path

### From Navigator

- All Navigator skills work unchanged
- App layer is additive (new workflows)
- Existing .agent/ structure compatible
- Update .nav-config.json for new features

### From Superpowers

- All Superpowers skills work unchanged
- OS layer adds context optimization
- No workflow changes required
- Initialize .agent/ with nav-init

### From Neither

- Start fresh with nav-init
- Both layers available immediately
- Guided onboarding (nav-onboard)
- Progressive learning

---

## Future Enhancements

### Planned

- Visual dashboard for .agent/ structure
- Real-time context usage monitoring
- Skill marketplace integration
- Team collaboration features

### Under Consideration

- Remote .agent/ sync (multi-machine)
- AI-generated integration points
- Custom trigger boundaries
- Layer versioning

---

## Summary

SuperNavigator's layered architecture provides:

✅ **Separation of Concerns**: OS vs App layers with clear boundaries
✅ **Implicit Integration**: Layers work together automatically
✅ **Token Efficiency**: 92% reduction via on-demand loading
✅ **Development Quality**: TDD enforcement, systematic processes
✅ **Extensibility**: Easy to add skills to either layer
✅ **User Control**: Configure integration level
✅ **Transparency**: Observable .agent/ state

The result: Sessions that finish what they start, with both efficiency and quality.
