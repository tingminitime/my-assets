---
description: Create well-formatted git commits with conventional commit messages and emoji
category: version-control-git
allowed-tools: Bash, Read, Glob
---

# Claude Command: Commit

This command helps you create well-formatted commits with conventional commit messages.

## Usage

To create a commit, just type:
```
/commit
```

Or with options:
```
/commit --no-verify
```

## Language Selection

Before proceeding with the commit process, present the user with language options:

1. **English (#en-US)** - Generate commit messages in English
2. **繁體中文 (#zh-TW)** - Generate commit messages in Traditional Chinese

Wait for the user to select their preferred language before proceeding with any commit operations.

## What This Command Does

1. **Select commit message language** (as described above)
2. Unless specified with `--no-verify`, automatically runs pre-commit checks:
   - Detect package manager (npm, pnpm, yarn, bun) and run appropriate commands
   - Run lint/format checks if available
   - Run build verification if build script exists
   - Update documentation if generation script exists
3. Checks which files are staged with `git status`
4. If 0 files are staged, automatically adds all modified and new files with `git add`
5. Performs a `git diff` to understand what changes are being committed
6. Analyzes the diff to determine if multiple distinct logical changes are present
7. If multiple distinct changes are detected, suggests breaking the commit into multiple smaller commits
8. **Displays the proposed commit message(s) and waits for user confirmation before executing `git commit`**
9. Only proceeds with the commit after receiving explicit approval from the user
10. Do NOT add Claude co-authorship footer to commits

## Best Practices for Commits

- **Verify before committing**: Ensure code is linted, builds correctly, and documentation is updated
- **Atomic commits**: Each commit should contain related changes that serve a single purpose
- **Split large changes**: If changes touch multiple concerns, split them into separate commits
- **Conventional commit format**: Use the format `<type>: <description>` where type is one of:
  - `feat`: A new feature
  - `fix`: A bug fix
  - `docs`: Documentation changes
  - `style`: Code style changes (formatting, etc)
  - `refactor`: Code changes that neither fix bugs nor add features
  - `perf`: Performance improvements
  - `test`: Adding or fixing tests
  - `chore`: Changes to the build process, tools, etc.
- **Present tense, imperative mood**: Write commit messages as commands (e.g., "add feature" not "added feature")
- **Concise first line**: Keep the first line under 72 characters
- **Bullet point body**: If a longer description is needed, write each point as a bullet (`-`) on its own line — never as a prose paragraph

## Language-Specific Guidelines

### English (#en-US)
- Use imperative mood: "add feature" not "adds feature" or "added feature"
- Keep descriptions concise and clear
- Example: `feat: add user authentication system`
- Example with body:
  ```
  feat: add user authentication system

  - implement JWT-based login and logout endpoints
  - add password hashing with bcrypt
  - include refresh token rotation logic
  ```

### 繁體中文 (#zh-TW)
- 使用簡潔的動詞開頭：「新增」、「修正」、「更新」等
- 保持描述清楚明確
- 範例：`feat: 新增使用者認證系統`
- 含內文範例：
  ```
  feat: 新增使用者認證系統

  - 實作基於 JWT 的登入與登出端點
  - 使用 bcrypt 進行密碼雜湊處理
  - 加入 refresh token 輪替邏輯
  ```

## User Confirmation Required

Before executing any `git commit` command, Claude will:
1. Present the complete commit message that will be used (in the selected language)
2. Show the list of staged files that will be included
3. Wait for explicit approval before proceeding

This ensures you have full control and can review the commit details before they are applied to your repository.