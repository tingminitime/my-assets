---
description: Automatically create and execute a git commit using the first suggested commit message
category: version-control-git
allowed-tools: Bash(git *)
---

# Create new fast commit task

This task uses the same logic as the commit task (.claude/commands/commit.md) but automatically selects the first suggested commit message without asking for confirmation.

## Language Selection

Before generating commit messages, present the user with language options:

1. **English (#en-US)** - Generate commit messages in English
2. **繁體中文 (#zh-TW)** - Generate commit messages in Traditional Chinese

Wait for the user to select their preferred language before proceeding.

## Commit Message Generation

After language selection:

- Generate 3 commit message suggestions following the same format as the commit task
- Use the selected language for all commit messages
- Automatically use the first suggestion without asking the user
- Immediately run `git commit -m` with the first message
- All other behaviors remain the same as the commit task (format, package names, staged files only)
- Do NOT add Claude co-authorship footer to commits

## User Confirmation Required

Before executing any `git commit` command, Claude will:
1. Present the complete commit message that will be used (in the selected language)
2. Show the list of staged files that will be included
3. Wait for explicit approval before proceeding

This ensures you have full control and can review the commit details before they are applied to your repository.