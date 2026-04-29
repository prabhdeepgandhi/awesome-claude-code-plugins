# System-Level Plugins

Install these in `~/.claude/plugins/` — available across ALL projects.

## Plugins

| Plugin | Command | What it does |
|--------|---------|-------------|
| **commit-commands** | `/commit`, `/commit-push-pr`, `/clean_gone` | Git workflow automation. One-shot commit, push, and PR creation |
| **double-check** | `/double-check` | Forces re-evaluation of completed work from multiple angles |
| **update-claudemd** | `/update-claudemd` | Auto-generates CLAUDE.md from git history and code changes |
| **explore** | `/explore <topic>` | Read planning docs + codebase to prepare for discussion |

## Installation

```bash
# Symlink all system plugins
for plugin in commit-commands double-check update-claudemd explore; do
  ln -sf "$(pwd)/system-plugins/$plugin" ~/.claude/plugins/$plugin
done
```

Or copy individual plugins:
```bash
cp -r system-plugins/commit-commands ~/.claude/plugins/
```
