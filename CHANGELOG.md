# Changelog

All notable changes to SuperNavigator will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [6.0.0] - 2026-01-20

### Added - SuperNavigator Unified Release

**Architecture**:
- ✨ Layered architecture combining Navigator (OS layer) + Superpowers (App layer)
- 🔗 Implicit integration via shared `.agent/` data store
- ⚙️ Enhanced `.nav-config.json` with both layer settings
- 📊 Unified documentation system (README.md, ARCHITECTURE.md)

**OS Layer** (from Navigator 5.2.0):
- 17 skills for context management, session persistence, Theory of Mind
- nav-init, nav-start, nav-onboard, nav-loop (session management)
- nav-profile, nav-marker, nav-compact, nav-diagnose (context/memory)
- nav-task, nav-sop, nav-skill-creator (documentation)
- nav-stats, nav-update-claude, nav-release, nav-upgrade, nav-install-multi-claude (project management)
- plugin-slash-command (plugin support)
- 92% token reduction through on-demand loading
- Theory of Mind features (verification checkpoints, bilateral modeling)
- Loop Mode with structured completion signals

**App Layer** (from Superpowers 4.0.3):
- 14 skills for development workflows, TDD, code review
- brainstorming, writing-plans (design)
- test-driven-development, using-git-worktrees, executing-plans (development)
- requesting-code-review, receiving-code-review, systematic-debugging (quality)
- dispatching-parallel-agents, subagent-driven-development (parallel)
- verification-before-completion, finishing-a-development-branch, writing-skills, using-superpowers (advanced)
- 100% test-first enforcement
- Systematic debugging and code review processes
- Parallel development with subagents

**Integration Features**:
- Auto-save markers before brainstorming (implicit trigger)
- Auto-index plans from writing-plans via nav-task (implicit trigger)
- Auto-compact at 85% context usage (implicit trigger)
- Auto-checkpoint on branch completion (implicit trigger)
- Workflow boundary triggers configurable in .nav-config.json
- Seamless data flow between layers via .agent/ storage

**Documentation**:
- Comprehensive README.md with layered architecture explanation
- ARCHITECTURE.md deep dive into OS + App layer design
- Migration guides from Navigator and Superpowers
- Getting started guide for new users
- Plugin-ready structure for future distribution

### Changed

**Directory Structure**:
- Skills organized by layer: `skills/os-layer/` and `skills/app-layer/`
- OS layer skills categorized: core, context-memory, documentation, project-management, plugin
- App layer skills categorized: design, development, quality, parallel, advanced
- Total 31 skills (17 OS + 14 App)

**Configuration**:
- `.nav-config.json` now includes `layers`, `app_layer_features`, and `implicit_integration` sections
- Version bumped from Navigator 5.2.0 / Superpowers 4.0.3 to unified 6.0.0

**Templates**:
- CLAUDE.md updated to reference SuperNavigator and both layers
- .nav-config.json template includes both layer settings
- DEVELOPMENT-README.md references App layer workflows

**Skills Modified**:
- `nav-init`: Creates both layer structures, enhanced config
- `nav-start`: Loads OS layer + injects using-superpowers (App layer)
- `using-superpowers`: References SuperNavigator architecture
- `brainstorming`: Notes nav-marker checkpoint creation
- `writing-plans`: Notes nav-task indexing
- `finishing-a-development-branch`: Notes nav-marker and nav-sop triggers

### Breaking Changes

- Directory structure changed from flat `skills/` to layered `skills/os-layer/` and `skills/app-layer/`
- `.nav-config.json` requires new sections for SuperNavigator features
- Skill paths in `.claude-plugin/plugin.json` updated to reflect new structure

### Migration

**From Navigator 5.x**:
1. Update directory structure to layered format
2. Update `.nav-config.json` with new sections
3. Update `.claude-plugin/plugin.json` with new skill paths
4. App layer workflows now available

**From Superpowers 4.x**:
1. Initialize `.agent/` structure with nav-init
2. Update `.nav-config.json` with Navigator settings
3. OS layer context management now available

**From Neither**:
1. Install SuperNavigator
2. Run "Initialize SuperNavigator in this project"
3. Run "Start my SuperNavigator session"
4. Both layers ready to use

---

## [5.2.0] - 2025-01-20 (Navigator)

### Added
- Loop Mode with structured completion signals
- NAVIGATOR_STATUS block for iteration tracking
- Dual-condition exit gates (heuristics + EXIT_SIGNAL)
- Stagnation detection (circuit breaker)
- Enhanced markers with belief state

### Changed
- Updated Theory of Mind features
- Improved context optimization strategies

---

## [4.0.3] - 2024-12-15 (Superpowers)

### Added
- Skills for TDD, code review, systematic debugging
- Brainstorming skill for design
- Writing-plans skill for implementation planning
- Parallel development with subagents

### Changed
- Improved skill discovery and invocation
- Enhanced documentation

---

## Version History

- **6.0.0** (2026-01-20): SuperNavigator unified release
- **5.2.0** (2025-01-20): Navigator Loop Mode
- **5.0.0** (2025-01-15): Navigator Theory of Mind integration
- **4.6.0** (2024-12-20): Navigator OpenTelemetry metrics
- **4.0.3** (2024-12-15): Superpowers core skills release
- **3.x**: Navigator context engineering foundation
- **2.x**: Superpowers TDD workflows
- **1.x**: Early Navigator prototypes

---

## Roadmap

### Planned for 6.1.0
- Visual dashboard for .agent/ structure
- Real-time context usage monitoring
- Team collaboration features
- Skill marketplace integration

### Under Consideration
- Remote .agent/ sync (multi-machine)
- AI-generated integration points
- Custom trigger boundaries per skill
- Layer versioning and compatibility

---

## Links

- [GitHub Repository](https://github.com/supernavigator/supernavigator) (future)
- [Documentation](README.md)
- [Architecture Guide](ARCHITECTURE.md)
- [License](LICENSE)

---

## Credits

SuperNavigator 6.0.0 is built on:
- **Navigator** by Aleks Petrov (https://github.com/alekspetrov/navigator) - OS Layer
- **Superpowers** by Jesse Vincent (https://github.com/obra/superpowers) - App Layer

Unified by SuperNavigator Contributors.
