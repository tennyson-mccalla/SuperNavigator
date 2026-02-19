# Installing SuperNavigator as a Claude Code Plugin

## Quick Install (One Command)

From **any project**, install SuperNavigator and get all 31 skills:

```bash
claude plugin marketplace add https://github.com/tennyson-mccalla/SuperNavigator
claude plugin install supernavigator
```

Then **restart Claude Code**.

That's it! All skills are now available in Claude Code.

---

## Verify Installation

In Claude Code, say:

```
"List available skills"
```

You should see SuperNavigator skills (nav-init, brainstorming, test-driven-development, etc.)

---

## First Use

### 1. Initialize Your Project

```
"Initialize SuperNavigator in this project"
```

This creates the `.agent/` directory structure and configuration.

### 2. Start Your Session

```
"Start my SuperNavigator session"
```

This loads both OS and App layers.

### 3. Start Coding

Pick any skill:
- `"Let's brainstorm a new feature"`
- `"Create implementation plan"`
- `"Set up test-driven development"`
- `"Request code review"`

---

## What You Get

**OS Layer (17 skills)**
- Context management, session persistence, metrics
- nav-init, nav-start, nav-loop, nav-profile, nav-marker, nav-compact, and more

**App Layer (14 skills)**
- TDD workflows, debugging, code review, parallel development
- brainstorming, writing-plans, test-driven-development, requesting-code-review, and more

---

## Managing the Plugin

### Update to Latest
```bash
claude plugin update supernavigator
```

### Remove
```bash
claude plugin uninstall supernavigator
```

### View Details
```bash
claude plugin info supernavigator
```

---

## Troubleshooting

### Plugin command not found
Make sure you have Claude Code CLI installed:
```bash
npm install -g @anthropic-ai/claude-code
```

### Skills not appearing after install
1. Restart Claude Code completely (not just closing the window)
2. Try: `claude plugin reinstall supernavigator`

### Permission issues
On macOS/Linux:
```bash
chmod -R 755 ~/.claude/plugins/supernavigator
```

---

## Next Steps

1. Install: Add marketplace and run `claude plugin install supernavigator`
2. Restart Claude Code
3. Initialize: `"Initialize SuperNavigator in this project"`
4. Start: `"Start my SuperNavigator session"`

Happy coding! 🚀
