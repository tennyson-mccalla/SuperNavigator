# [Project Name] - Claude Code Configuration

## Context

[Brief project description - explain what this project does]

**Tech Stack**: [List your technologies, e.g., Next.js, TypeScript, PostgreSQL]

**Core Principle**: [Key architectural principle, e.g., "API-first design with type safety"]

**Last Updated**: [Date]
**SuperNavigator Version**: 6.0.0

---

## SuperNavigator Quick Start

**Every session begins with**:
```
"Start my SuperNavigator session"
```

This loads:
- **OS Layer** (Navigator): `.agent/DEVELOPMENT-README.md` context index
- **App Layer** (Superpowers): TDD workflows, code review, systematic debugging
- Both layers work together via implicit integration

**Core workflow**:
1. **Start session** → Loads both layers automatically
2. **Design** → Use brainstorming skill for features
3. **Plan** → Use writing-plans for implementation
4. **Implement** → TDD with test-driven-development skill
5. **Review** → Use requesting-code-review
6. **Complete** → Use finishing-a-development-branch

**Natural language commands** (OS Layer):
- "Start my SuperNavigator session" (begin work)
- "Archive TASK-XX documentation" (after completion)
- "Create an SOP for debugging [issue]" (document solution)
- "Create a context marker" (save progress)

**App Layer workflows** (automatic):
- Brainstorming creates checkpoints
- Writing-plans indexes in nav-task
- TDD enforces test-first
- Code review validates against spec

**For full SuperNavigator workflow**: See plugin's root README.md or ARCHITECTURE.md

---

## Project-Specific Code Standards

[Customize for your project's framework and patterns]

### General Standards
- **Architecture**: KISS, DRY, SOLID principles
- **TypeScript**: Strict mode, no `any` without justification
- **Line Length**: Max 100 characters
- **Testing**: High coverage (backend 90%+, frontend 85%+)

### Framework-Specific Patterns

**Example: Next.js/React**
- Server Components by default (no 'use client' unless interactive)
- Functional components only, no classes
- TailwindCSS v4 for styling (no inline styles)
- Data fetching on server (async/await in components)

**Example: Python/Django**
- Type hints on all functions
- Black formatter (88 char line length)
- Class-Based Views preferred
- Django ORM (avoid raw SQL without justification)

**Example: Go**
- Standard library first, minimize dependencies
- Errors as values (no exceptions)
- Interfaces for abstraction
- gofmt + golangci-lint

[Replace examples above with your actual tech stack guidelines]

---

## Forbidden Actions

### Navigator Violations (HIGHEST PRIORITY)
- ❌ NEVER wait for explicit commit prompts (autonomous mode - commit when complete)
- ❌ NEVER leave tickets open after completion
- ❌ NEVER skip documentation after features
- ❌ NEVER load all `.agent/` docs at once (defeats token optimization)
- ❌ NEVER skip reading DEVELOPMENT-README.md navigator

### General Violations
- ❌ No Claude Code mentions in commits/code
- ❌ No package.json modifications without approval
- ❌ Never commit secrets/API keys/.env files
- ❌ Don't delete tests without replacement

[Add project-specific violations here]

---

## Documentation Structure

```
.agent/
├── DEVELOPMENT-README.md      # Navigator (always load first)
├── tasks/                     # Implementation plans
├── system/                    # Architecture docs
└── sops/                      # Standard Operating Procedures
    ├── integrations/
    ├── debugging/
    ├── development/
    └── deployment/
```

**Token-efficient loading**:
- Navigator: ~2k tokens (always)
- Current task: ~3k tokens (as needed)
- System docs: ~5k tokens (when relevant)
- SOPs: ~2k tokens (if required)
- **Total**: ~12k vs ~150k loading everything

---

## Project Management Integration

[Configure based on your setup - remove this section if not using PM integration]

**Configured Tool**: [Linear / GitHub Issues / Jira / GitLab / None]

**Workflow**:
1. Read ticket via PM tool
2. Generate implementation plan → `.agent/tasks/`
3. Implement features
4. Update system docs if architecture changes
5. Complete → "Archive TASK-XX documentation" (auto-closes ticket)
6. Notify team (if chat integration configured)

---

## Configuration

Navigator config in `.agent/.nav-config.json`:

```json
{
  "version": "4.6.0",
  "project_management": "none",
  "task_prefix": "TASK",
  "team_chat": "none",
  "auto_load_navigator": true,
  "compact_strategy": "conservative"
}
```

**Customize after initialization**:
- `project_management`: "linear" | "github" | "jira" | "gitlab" | "none"
- `task_prefix`: Your ticket prefix (e.g., "PROJ", "DEV")
- `team_chat`: "slack" | "discord" | "none"

---

## Commit Guidelines

- **Format**: `type(scope): description`
- **Reference ticket**: `feat(auth): implement OAuth login TASK-XX`
- **Types**: feat, fix, docs, refactor, test, chore
- No Claude Code mentions in commits
- Concise and descriptive

---

## Success Metrics

### Context Efficiency
- <70% token usage for typical tasks
- <12k tokens loaded per session
- 10+ exchanges without compact
- Zero session restarts during features

### Documentation Coverage
- 100% completed features have task docs
- 90%+ integrations have SOPs
- System docs updated within 24h
- Zero repeated mistakes

---

**For complete Navigator documentation**:
- `.agent/DEVELOPMENT-README.md` (project navigator)
- Plugin's root CLAUDE.md (full workflow reference)
