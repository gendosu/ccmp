# Git Operations Specialist - Detailed Reference

This document provides detailed command references, advanced operations, and troubleshooting guidance for the Git Operations Specialist skill.

## Advanced Git Operations Command Reference / 高度なGit操作コマンド集

### Interactive Rebase / インタラクティブリベース

**Purpose / 目的**: Rewrite commit history, squash commits, reorder commits, edit commit messages

**Basic Interactive Rebase**:
```bash
# Rebase last N commits
git rebase -i HEAD~3

# Rebase from a specific commit
git rebase -i <commit-hash>

# Rebase onto a branch
git rebase -i main
```

**Interactive Commands / 対話的コマンド**:
- `pick` - Use commit as-is (そのままコミットを使用)
- `reword` - Use commit, but edit message (コミットを使用するがメッセージを編集)
- `edit` - Use commit, but stop for amending (コミットを使用するが修正のため停止)
- `squash` - Combine with previous commit (前のコミットと結合)
- `fixup` - Like squash, but discard message (squashと同様だがメッセージは破棄)
- `drop` - Remove commit (コミットを削除)

**Example Workflow / ワークフロー例**:
```bash
# Start interactive rebase
git rebase -i HEAD~5

# In editor, change:
pick abc123 feat: Add feature A
pick def456 fix: typo
pick ghi789 feat: Add feature B
pick jkl012 fix: another typo
pick mno345 docs: Update README

# To:
pick abc123 feat: Add feature A
fixup def456 fix: typo
pick ghi789 feat: Add feature B
fixup jkl012 fix: another typo
pick mno345 docs: Update README

# Save and exit
# Git will automatically squash the fixup commits
```

**Handling Conflicts During Rebase**:
```bash
# If conflicts occur
git status  # See conflicted files
# Resolve conflicts manually
git add <resolved-files>
git rebase --continue

# To abort rebase
git rebase --abort
```

### Cherry-pick / チェリーピック

**Purpose / 目的**: Apply specific commits from one branch to another

**Basic Cherry-pick**:
```bash
# Apply single commit
git cherry-pick <commit-hash>

# Apply multiple commits
git cherry-pick <commit1> <commit2> <commit3>

# Apply range of commits (exclusive of commit1, inclusive of commit2)
git cherry-pick commit1..commit2
```

**Cherry-pick with Options**:
```bash
# Cherry-pick without committing (stage only)
git cherry-pick -n <commit-hash>

# Cherry-pick and edit commit message
git cherry-pick --edit <commit-hash>

# Cherry-pick with signoff
git cherry-pick -s <commit-hash>
```

**Handling Cherry-pick Conflicts**:
```bash
# If conflicts occur
git status
# Resolve conflicts
git add <resolved-files>
git cherry-pick --continue

# To abort cherry-pick
git cherry-pick --abort
```

### Stash Management / Stash管理

**Purpose / 目的**: Temporarily save uncommitted changes

**Basic Stash Operations**:
```bash
# Save current changes
git stash
git stash push -m "WIP: feature implementation"

# List all stashes
git stash list

# Show stash contents
git stash show stash@{0}
git stash show -p stash@{0}  # Show full diff

# Apply stash (keep in stash list)
git stash apply stash@{0}

# Pop stash (apply and remove from list)
git stash pop

# Drop specific stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
```

**Advanced Stash Operations**:
```bash
# Stash including untracked files
git stash -u

# Stash including ignored files
git stash -a

# Stash specific files
git stash push -m "message" path/to/file1 path/to/file2

# Create branch from stash
git stash branch <new-branch-name> stash@{0}
```

### Submodule Operations / Submodule操作

**Purpose / 目的**: Manage Git repositories within a Git repository

**Add Submodule**:
```bash
git submodule add <repository-url> <path>
git submodule add https://github.com/user/repo.git libs/external-lib
```

**Initialize and Update Submodules**:
```bash
# After cloning a repo with submodules
git submodule init
git submodule update

# Or in one command
git submodule update --init

# Update all submodules to latest
git submodule update --remote
```

**Remove Submodule**:
```bash
# 1. Remove from .gitmodules
git config -f .gitmodules --remove-section submodule.<path>

# 2. Remove from .git/config
git config -f .git/config --remove-section submodule.<path>

# 3. Remove from working tree
git rm --cached <path>
rm -rf <path>

# 4. Commit changes
git commit -m "chore: サブモジュールを削除"
```

## GitHub CLI Advanced Operations / GitHub CLI 高度な操作

### GraphQL API Examples / GraphQL API活用例

**Fetch Pull Request Details with Comments**:
```bash
gh api graphql -f query='
  query($owner: String!, $repo: String!, $number: Int!) {
    repository(owner: $owner, name: $repo) {
      pullRequest(number: $number) {
        title
        body
        state
        author {
          login
        }
        comments(last: 20) {
          nodes {
            body
            author {
              login
            }
            createdAt
          }
        }
        reviews(last: 10) {
          nodes {
            state
            author {
              login
            }
            body
          }
        }
      }
    }
  }
' -f owner='owner-name' -f repo='repo-name' -F number=123
```

**Fetch Repository Issues with Labels**:
```bash
gh api graphql -f query='
  query($owner: String!, $repo: String!) {
    repository(owner: $owner, name: $repo) {
      issues(first: 50, states: OPEN) {
        nodes {
          number
          title
          labels(first: 10) {
            nodes {
              name
            }
          }
          author {
            login
          }
        }
      }
    }
  }
' -f owner='owner-name' -f repo='repo-name'
```

**Fetch Commit History**:
```bash
gh api graphql -f query='
  query($owner: String!, $repo: String!, $branch: String!) {
    repository(owner: $owner, name: $repo) {
      ref(qualifiedName: $branch) {
        target {
          ... on Commit {
            history(first: 50) {
              nodes {
                oid
                message
                author {
                  name
                  email
                  date
                }
              }
            }
          }
        }
      }
    }
  }
' -f owner='owner-name' -f repo='repo-name' -f branch='refs/heads/main'
```

### Complex Data Retrieval Patterns / 複雑なデータ取得パターン

**Create Issue with JSON Input File**:
```bash
# Create input file
cat > ./tmp/issue.json <<'EOF'
{
  "title": "バグ報告: ログイン機能エラー",
  "body": "## 問題の説明\n\nログイン時にエラーが発生します。\n\n## 再現手順\n\n1. ログイン画面を開く\n2. 資格情報を入力\n3. ログインボタンをクリック\n\n## 期待される動作\n\nログインが成功する\n\n## 実際の動作\n\nエラーメッセージが表示される",
  "labels": ["bug", "high-priority"]
}
EOF

# Create issue using file
gh api repos/:owner/:repo/issues --method POST --input ./tmp/issue.json
```

**Update PR with File**:
```bash
# Create PR body file
cat > ./tmp/pr-update.md <<'EOF'
## 更新内容

- バグ修正を追加
- テストケースを追加
- ドキュメントを更新

## テスト結果

- [x] ユニットテスト: 合格
- [x] 統合テスト: 合格
- [x] E2Eテスト: 合格
EOF

# Update PR
gh pr edit 123 --body-file ./tmp/pr-update.md
```

**Batch Operations**:
```bash
# Close multiple issues
for issue in 45 46 47; do
  gh issue close $issue -c "修正済み"
done

# Add label to multiple PRs
for pr in $(gh pr list --state open --json number -q '.[].number'); do
  gh pr edit $pr --add-label "needs-review"
done
```

## Troubleshooting Details / トラブルシューティング詳細

### Conflict Resolution Patterns / コンフリクト解決パターン

**Understanding Conflict Markers / コンフリクトマーカーの理解**:
```
<<<<<<< HEAD
Current branch changes
=======
Incoming branch changes
>>>>>>> branch-name
```

**Strategy 1: Accept Ours (現在のブランチを優先)**:
```bash
git checkout --ours <file>
git add <file>
```

**Strategy 2: Accept Theirs (取り込むブランチを優先)**:
```bash
git checkout --theirs <file>
git add <file>
```

**Strategy 3: Manual Resolution (手動解決)**:
```bash
# 1. Open file in editor
# 2. Edit to resolve conflicts
# 3. Remove conflict markers
# 4. Save file
git add <file>
```

**Using Merge Tools / マージツールの使用**:
```bash
# Configure merge tool (if not already configured)
git config merge.tool vimdiff  # or meld, kdiff3, etc.

# Use merge tool
git mergetool
```

**Abort Merge**:
```bash
git merge --abort
```

### Repository Diagnostics and Repair / リポジトリ診断と修復

**Check Repository Integrity / リポジトリ整合性チェック**:
```bash
# File system check
git fsck --full

# Check for unreachable objects
git fsck --unreachable
```

**Recover Lost Commits / 失われたコミットの回復**:
```bash
# View reflog (shows all HEAD movements)
git reflog

# Recover commit
git cherry-pick <commit-hash-from-reflog>

# Or create branch from lost commit
git branch recovered-branch <commit-hash>
```

**Clean Repository / リポジトリクリーンアップ**:
```bash
# Preview what will be removed
git clean -n

# Remove untracked files
git clean -f

# Remove untracked files and directories
git clean -fd

# Remove ignored files too
git clean -fdx
```

**Garbage Collection / ガベージコレクション**:
```bash
# Run garbage collection
git gc

# Aggressive garbage collection
git gc --aggressive --prune=now
```

**Repair Corrupted Repository**:
```bash
# 1. Backup first
cp -r .git .git-backup

# 2. Try to recover
git fsck --full

# 3. If objects are missing, try to restore from remote
git fetch --all

# 4. Reset to known good state
git reset --hard origin/main
```

### Common Errors and Solutions / よくあるエラーと解決方法

**Error: "fatal: refusing to merge unrelated histories"**:
```bash
# Solution: Allow unrelated histories
git merge <branch> --allow-unrelated-histories
```

**Error: "error: failed to push some refs"**:
```bash
# Solution 1: Pull first (recommended)
git pull --rebase origin main
git push

# Solution 2: Force push (use with caution)
git push --force-with-lease
```

**Error: "error: Your local changes would be overwritten by merge"**:
```bash
# Solution 1: Stash changes
git stash
git pull
git stash pop

# Solution 2: Commit changes first
git add .
git commit -m "WIP: 作業中の変更を保存"
git pull
```

**Error: "fatal: Not possible to fast-forward, aborting"**:
```bash
# Solution: Disable fast-forward requirement
git pull --no-ff

# Or configure globally
git config pull.ff false
```

**Error: "fatal: The current branch has no upstream branch"**:
```bash
# Solution: Set upstream branch
git push -u origin <branch-name>
```

**Detached HEAD State**:
```bash
# Check current state
git status

# Solution 1: Create branch from current position
git checkout -b new-branch-name

# Solution 2: Return to previous branch
git checkout main
```

**Large File Error**:
```bash
# Remove large file from history
git filter-branch --tree-filter 'rm -f path/to/large/file' HEAD

# Or use BFG Repo-Cleaner (faster)
# Download from https://rtyley.github.io/bfg-repo-cleaner/
java -jar bfg.jar --delete-files large-file.bin
git reflog expire --expire=now --all
git gc --prune=now --aggressive
```

---

## Additional Resources / 追加リソース

### Official Documentation / 公式ドキュメント
- Git Official Documentation: https://git-scm.com/doc
- GitHub CLI Documentation: https://cli.github.com/manual/
- GitHub GraphQL API: https://docs.github.com/en/graphql

### Recommended Reading / 推奨読書
- Pro Git Book: https://git-scm.com/book/en/v2
- Git Best Practices: https://www.git-tower.com/learn/git/ebook/en/command-line/appendix/best-practices

### Project-Specific Documentation / プロジェクト固有ドキュメント
- Coding Conventions: `docs/ai/development/coding-conventions.md`
- GitHub PR Guidelines: `docs/ai/workflows/300-github-pr.md`
- Security Guidelines: `docs/ai/development/security-guidelines.md`
