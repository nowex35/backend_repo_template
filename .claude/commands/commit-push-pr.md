# Ship: Commit, Push, and Create PR

Commit all changes, push to remote, and create a pull request in one workflow.

## Workflow

### 1. Check current state

Run `git status` (without -uall flag) and `git diff` to understand what has changed. If there are no changes, inform the user and stop.

### 2. Analyze changes

Run `git diff` and `git diff --cached` to review all staged and unstaged changes. Understand the nature of each change (new feature, bug fix, refactoring, etc.).

### 3. Stage and commit

- Stage all relevant changed files individually by name (do NOT use `git add -A` or `git add .`). Never stage files that likely contain secrets (.env, credentials, etc.).
- Write a concise commit message in English that focuses on "why" rather than "what", following the project's Tidy First methodology.
- End the commit message with: `Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>`
- Use a HEREDOC for the commit message to ensure correct formatting.

### 4. Create branch if needed

If currently on `main`, create a new descriptive branch before pushing:
- Branch name format: `feat/short-description`, `fix/short-description`, or `refactor/short-description`
- Ask the user for the branch name if the appropriate name is unclear.

### 5. Push to remote

Push the current branch to origin with the `-u` flag:
```
git push -u origin <branch-name>
```

### 6. Create Pull Request

Create a PR using `gh pr create` with the project's PR template structure. The PR title and body must be in English (per AGENTS.md rules). Use the following format:

```
gh pr create --title "<concise title under 70 chars>" --body "$(cat <<'EOF'
## 議論/問題提起の場所
<link to issue, Discord, Google Doc, or "N/A">

## なぜこの変更をするのか(why)
<explain why this change is needed>

## どうやって実現するのか(How)
<explain the implementation approach>

## 実装上の懸念(特にレビューしてほしい部分など)
<areas of concern or "None">

## 動作確認
レビュワーは以下の点をチェック
- [ ] <verification items>

## 備考
<additional notes or "None">

🤖 Generated with [Claude Code](https://claude.com/claude-code)
EOF
)"
```

### 7. Report result

Show the user the created PR URL and a summary of what was done.

## Rules

- All commit messages, PR titles must be in English (per AGENTS.md)
- PR body sections use the Japanese template headers from PULL_REQUEST_TEMPLATE but content can be in English
- Never commit .env or credential files
- Never force push
- Never amend existing commits
- If any step fails, stop and report the error to the user
