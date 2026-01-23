# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Context

**SuperNavigator** is a Claude Code plugin that combines two frameworks:
- **OS Layer (Navigator)**: Context management, session persistence, Theory of Mind (17 skills)
- **App Layer (Superpowers)**: TDD workflows, debugging, code review (14 skills)

**Architecture**: Layered system with implicit integration via `.agent/` data store
**Version**: 6.0.0 (Navigator 5.2.0 + Superpowers 4.0.3)
**Repository**: https://github.com/dkyazzentwatwa/SuperNavigator

---

## Installation (For Users)

Users install SuperNavigator via:
```bash
claude plugin install https://github.com/dkyazzentwatwa/SuperNavigator
```

This installs all 31 skills defined in `.claude-plugin/plugin.json`.

---

## Repository Structure

### Critical Directories

**Skills (Main Product)**:
```
skills/
├── os-layer/              # Navigator - 17 skills
│   ├── core/              # nav-init, nav-start, nav-onboard, nav-loop
│   ├── context-memory/    # nav-profile, nav-marker, nav-compact, nav-diagnose
│   ├── documentation/     # nav-task, nav-sop, nav-skill-creator
│   ├── project-management/# nav-stats, nav-update-claude, nav-release, nav-upgrade
│   └── plugin/            # plugin-slash-command
│
└── app-layer/             # Superpowers - 14 skills
    ├── design/            # brainstorming, writing-plans
    ├── development/       # test-driven-development, using-git-worktrees, executing-plans
    ├── quality/           # requesting-code-review, receiving-code-review, systematic-debugging
    ├── parallel/          # dispatching-parallel-agents, subagent-driven-development
    └── advanced/          # verification-before-completion, finishing-a-development-branch, writing-skills, using-superpowers
```

**Each skill directory contains**:
- `SKILL.md` (required) - Main skill documentation with YAML frontmatter
- Supporting files (functions/, templates/, examples/) - Optional helpers

**Plugin Configuration**:
```
.claude-plugin/
├── plugin.json          # Manifest with all 31 skill paths (critical for installation)
├── marketplace.json     # Marketplace metadata
└── README.md           # Plugin installation instructions
```

**Documentation**:
```
docs/
├── guides/             # Getting started, OS/App layer guides
├── migration/          # From Navigator/Superpowers
└── PLUGIN-INSTALLATION.md  # Installation guide for users
```

**Templates**:
```
templates/
└── CLAUDE.md          # Template for users' projects
```

---

## Layered Architecture (Critical Concept)

**DO NOT treat this as a monolithic skill collection.**

### OS Layer (Navigator)
- **Purpose**: Context efficiency - load only what's needed
- **Triggers**: Session start, context threshold (85%), completion
- **Reads**: `.agent/DEVELOPMENT-README.md`, markers, profiles
- **Writes**: `.agent/markers/`, `.agent/profiles/`, index updates

### App Layer (Superpowers)
- **Purpose**: Development workflows - TDD, debugging, review
- **Triggers**: User requests ("brainstorm...", "create plan...", "review code...")
- **Reads**: Git state, test results, plan files
- **Writes**: `docs/plans/`, `.agent/tasks/`, `.agent/sops/`, `.agent/system/`

### Integration Layer
- **Medium**: `.agent/` directory (shared data store)
- **Method**: Implicit triggers at workflow boundaries
- **Config**: `.agent/.nav-config.json` controls integration behavior

**Key insight**: Layers communicate through `.agent/` files, not direct skill-to-skill calls.

---

## Skill Development Standards

### YAML Frontmatter (Required)

Every `SKILL.md` MUST have:
```yaml
---
name: skill-name-with-hyphens
description: Use when [specific triggering conditions]. Third person. Max 500 chars.
---
```

**Critical Rules**:
- `name`: Letters, numbers, hyphens only (no parentheses, spaces, underscores)
- `description`: Start with "Use when...", describe TRIGGERS not workflow
- Max 1024 chars total for frontmatter
- Third person voice

**Why description matters**: Claude reads this to decide which skills to load. Poor descriptions = skills never discovered.

### Skill Creation Workflow

**From `skills/app-layer/advanced/writing-skills/SKILL.md`**:

1. **RED Phase** (failing test):
   - Create pressure scenarios without the skill
   - Document exact rationalizations/failures
   - Identify patterns

2. **GREEN Phase** (write skill):
   - Address specific baseline failures
   - Write minimal skill content
   - Test scenarios WITH skill - verify compliance

3. **REFACTOR Phase** (close loopholes):
   - Identify new rationalizations
   - Add explicit counters (for discipline skills)
   - Build rationalization table
   - Re-test until bulletproof

**Iron Law**: NO SKILL WITHOUT FAILING TEST FIRST
- Applies to new skills AND edits
- No exceptions
- Delete untested code

### Adding New Skills

**To OS Layer**:
1. Create in `skills/os-layer/{category}/{skill-name}/SKILL.md`
2. Add path to `.claude-plugin/plugin.json` skills array
3. Document in `docs/guides/OS-LAYER-GUIDE.md`
4. Test with nav-start

**To App Layer**:
1. Create in `skills/app-layer/{category}/{skill-name}/SKILL.md`
2. Add path to `.claude-plugin/plugin.json` skills array
3. Add integration section (how it works with OS layer)
4. Document in `docs/guides/APP-LAYER-GUIDE.md`
5. Test workflow end-to-end

**Critical**: Update `.claude-plugin/plugin.json` or skill won't install for users.

---

## Plugin Configuration Management

### plugin.json Structure

```json
{
  "name": "supernavigator",
  "version": "6.0.0",
  "description": "...",
  "repository": "https://github.com/dkyazzentwatwa/SuperNavigator",
  "skills": [
    "./skills/os-layer/core/nav-init",
    "./skills/os-layer/core/nav-start",
    ...all 31 skill paths...
  ]
}
```

**When adding a skill**:
1. Create the skill directory and SKILL.md
2. Add relative path to `skills` array
3. Paths are relative to repo root
4. Order doesn't matter (keep logical grouping)

**When removing a skill**:
1. Remove from `skills` array
2. Consider deprecation notice first
3. Update CHANGELOG.md

---

## Documentation Philosophy

### ARCHITECTURE.md
- **Purpose**: Deep dive into layered design
- **Audience**: Users wanting to understand how it works
- **Update when**: Adding integration points, changing layer boundaries

### README.md
- **Purpose**: Quick start and value proposition
- **Audience**: First-time users, GitHub visitors
- **Keep**: Installation command, key features, example workflow

### docs/guides/
- **OS-LAYER-GUIDE.md**: Navigator features and usage
- **APP-LAYER-GUIDE.md**: Superpowers workflows
- **GETTING-STARTED.md**: First session walkthrough
- **PLUGIN-INSTALLATION.md**: Installation instructions

**When to update**:
- New skill added → Update relevant guide
- Integration behavior changed → Update IMPLICIT-INTEGRATION.md
- Breaking change → Update migration guides

---

## Version Management

### Semantic Versioning

- **Major** (X.0.0): Breaking changes to skill APIs or .agent/ structure
- **Minor** (6.X.0): New skills, new features, non-breaking changes
- **Patch** (6.0.X): Bug fixes, documentation updates

### Files to Update on Version Change

1. `.claude-plugin/plugin.json` - `version` field
2. `.claude-plugin/marketplace.json` - `version` and `changelog` section
3. `README.md` - Version badge and release date
4. `CHANGELOG.md` - Document changes

**Coordination**:
- OS layer version (Navigator): Currently 5.2.0
- App layer version (Superpowers): Currently 4.0.3
- SuperNavigator version: 6.0.0 (independent)

---

## Common Tasks

### Testing a Skill Locally

1. Edit skill in `skills/{layer}/{category}/{name}/SKILL.md`
2. Ensure `.claude-plugin/plugin.json` has the path
3. Link plugin locally:
   ```bash
   ln -s $(pwd) ~/.claude/plugins/supernavigator
   ```
4. Restart Claude Code
5. Test skill invocation

### Validating Skill YAML

Check frontmatter format:
```bash
head -10 skills/os-layer/core/nav-init/SKILL.md
```

Should see:
```yaml
---
name: nav-init
description: Use when initializing SuperNavigator in a new project...
---
```

### Publishing Changes

1. Commit changes to main branch
2. Users update with: `claude plugin update supernavigator`
3. Or reinstall: `claude plugin install https://github.com/dkyazzentwatwa/SuperNavigator`

---

## Integration Testing

### Implicit Integration Points (Critical)

Test these workflow boundaries:

1. **Before brainstorming** → nav-marker checkpoint created
2. **After writing-plans** → nav-task indexes plan
3. **After requesting-code-review** → nav-compact if context >85%
4. **On finishing-a-development-branch** → nav-marker + nav-sop suggestion

**How to test**:
1. Initialize project with nav-init
2. Run workflow skill (e.g., brainstorming)
3. Verify OS layer trigger occurred
4. Check `.agent/` for expected writes

### .agent/ Structure Validation

After integration test, verify:
```
.agent/
├── DEVELOPMENT-README.md   # Updated index
├── tasks/TASK-*.md         # Plan from writing-plans
├── markers/checkpoint-*.md # From nav-marker
└── .nav-config.json        # Config intact
```

---

## Forbidden Actions

### Plugin Development
- ❌ NEVER add skill without updating `.claude-plugin/plugin.json`
- ❌ NEVER use spaces, underscores, or special chars in skill names
- ❌ NEVER put workflow summary in skill description (triggers only)
- ❌ NEVER skip TDD for skill creation (RED-GREEN-REFACTOR required)
- ❌ NEVER break layered architecture (no cross-layer skill dependencies)

### Skill Content
- ❌ NEVER include emojis unless user requests
- ❌ NEVER create multiple example files for same pattern (one excellent example)
- ❌ NEVER use flowcharts for reference material (tables instead)
- ❌ NEVER exceed 500 words without justification (token efficiency)

### Version Management
- ❌ NEVER change version without updating all 4 files (see Version Management)
- ❌ NEVER break `.agent/` structure compatibility in patch versions
- ❌ NEVER skip CHANGELOG.md updates

---

## Development Principles

From **OS Layer** (Navigator):
- Load what you need, when you need it (token efficiency first)
- Theory of Mind - remember user preferences
- Metrics-driven optimization (OpenTelemetry)

From **App Layer** (Superpowers):
- Test-Driven Development (write tests first, always)
- Systematic over ad-hoc (process over guessing)
- Complexity reduction (simplicity as primary goal)
- Evidence over claims (verify before declaring success)

**Unified Principle**: Layered architecture enables specialization. Integration should be implicit, not manual.

---

## Key Files Reference

- `ARCHITECTURE.md` - Layered design deep dive
- `README.md` - User-facing quick start
- `.claude-plugin/plugin.json` - Plugin manifest (31 skill paths)
- `skills/app-layer/advanced/writing-skills/SKILL.md` - Skill creation methodology
- `docs/PLUGIN-INSTALLATION.md` - Installation guide for users
- `CHANGELOG.md` - Version history

---

## Support Resources

- GitHub: https://github.com/dkyazzentwatwa/SuperNavigator
- Issues: Report bugs and feature requests
- Discussions: User questions and feedback

**Built on**: Navigator (Aleks Petrov) + Superpowers (Jesse Vincent)
