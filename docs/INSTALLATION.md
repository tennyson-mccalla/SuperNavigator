# Installation Guide

## Quick Install (Recommended)

### Step 1: Clone the Repository

```bash
git clone https://github.com/supernavigator/supernavigator.git
cd supernavigator
```

### Step 2: Run the Installer

**macOS / Linux:**
```bash
./install.sh
```

**Windows (PowerShell):**
```powershell
# Make sure you have Git Bash or WSL installed, then run
bash install.sh
```

### Step 3: Restart Claude Code

Close and reopen Claude Code to load the newly installed skills.

### Step 4: Initialize Your Project

In Claude Code, run:
```
"Initialize SuperNavigator in this project"
```

---

## Manual Installation

If the installer script doesn't work for your setup, you can manually install:

### 1. Find Your Skills Directory

**macOS:**
```bash
~/.claude/plugins/superpowers-marketplace/superpowers/4.0.3/skills/
```

**Linux:**
```bash
~/.claude/plugins/superpowers-marketplace/superpowers/4.0.3/skills/
```

**Windows:**
```
%APPDATA%\.claude\plugins\superpowers-marketplace\superpowers\4.0.3\skills\
```

### 2. Copy Skills

```bash
# From the SuperNavigator repo directory
cp -r skills/os-layer/* ~/.claude/plugins/superpowers-marketplace/superpowers/4.0.3/skills/
cp -r skills/app-layer/* ~/.claude/plugins/superpowers-marketplace/superpowers/4.0.3/skills/
```

### 3. Restart Claude Code

---

## Verification

After installation, verify SuperNavigator is loaded:

```
"List available skills"
```

You should see:
- **OS Layer:** nav-init, nav-start, nav-onboard, nav-loop, nav-profile, nav-marker, nav-compact, nav-diagnose, nav-task, nav-sop, nav-stats, and more
- **App Layer:** brainstorming, writing-plans, test-driven-development, using-git-worktrees, executing-plans, requesting-code-review, systematic-debugging, and more

---

## Updating SuperNavigator

### From Git (Recommended)

```bash
cd supernavigator
git pull
./install.sh
```

Then restart Claude Code.

### From Zip Download

1. Download the latest [release](https://github.com/supernavigator/supernavigator/releases)
2. Extract and run `./install.sh`
3. Restart Claude Code

---

## Troubleshooting

### "Skills not appearing in Claude Code"

1. **Verify installation location:**
   ```bash
   ls -la ~/.claude/plugins/superpowers-marketplace/superpowers/4.0.3/skills/
   ```

2. **Check for duplicates:** Some skills may exist in both old and new locations. Remove old versions first:
   ```bash
   # Look for existing superpowers skills
   find ~/.claude -name "writing-plans" -o -name "test-driven-development"
   ```

3. **Clear cache and restart:** Close Claude Code, wait 10 seconds, reopen.

### "install.sh: command not found"

Make sure the script is executable:
```bash
chmod +x install.sh
./install.sh
```

### "Permission denied"

On Linux/macOS, ensure the script is executable:
```bash
chmod +x install.sh
```

### "Skills installed but not loading"

1. Verify the skill YAML frontmatter is correct:
   ```bash
   head -10 ~/.claude/plugins/superpowers-marketplace/superpowers/4.0.3/skills/nav-init/SKILL.md
   ```

2. Restart Claude Code completely (not just closing the terminal)

3. Try re-running the installer:
   ```bash
   ./install.sh
   ```

---

## What Gets Installed

### OS Layer (17 skills)

**Core:**
- `nav-init` - Initialize SuperNavigator
- `nav-start` - Start a session
- `nav-onboard` - Onboarding workflow
- `nav-loop` - Autonomous task loop

**Context & Memory:**
- `nav-profile` - User preferences
- `nav-marker` - Session checkpoints
- `nav-compact` - Context pruning
- `nav-diagnose` - Quality detection

**Documentation:**
- `nav-task` - Task indexing
- `nav-sop` - SOP documentation
- `nav-skill-creator` - Skill creation helper

**Project Management:**
- `nav-stats` - Metrics and reporting
- `nav-update-claude` - Version updates
- `nav-release` - Release management
- `nav-upgrade` - Plugin upgrades
- `nav-install-multi-claude` - Multi-version support

**Plugin:**
- `plugin-slash-command` - Custom commands

### App Layer (14 skills)

**Design:**
- `brainstorming` - Ideation and refinement
- `writing-plans` - Implementation planning

**Development:**
- `test-driven-development` - TDD workflow
- `using-git-worktrees` - Isolated workspaces
- `executing-plans` - Plan execution

**Quality:**
- `requesting-code-review` - Code review requests
- `receiving-code-review` - Receiving feedback
- `systematic-debugging` - Root-cause debugging

**Parallel:**
- `dispatching-parallel-agents` - Concurrent tasks
- `subagent-driven-development` - Subagent workflows

**Advanced:**
- `verification-before-completion` - Quality gates
- `finishing-a-development-branch` - Branch completion
- `writing-skills` - Skill authoring
- `using-superpowers` - Superpowers guide

---

## Next Steps

After installation:

1. **Read the Getting Started Guide:** `docs/guides/GETTING-STARTED.md`
2. **Initialize a project:** `"Initialize SuperNavigator in this project"`
3. **Start your first session:** `"Start my SuperNavigator session"`

Happy coding! 🚀
