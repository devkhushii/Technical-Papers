# Git – Quick Revision Cheat Sheet

## 1. Git Setup and Configuration

| Command | Purpose |
|---|---|
| `git --version` | Check Git version |
| `git config --global user.name "Name"` | Set username |
| `git config --global user.email "email"` | Set email |
| `git config --list` | View Git configuration |
| `git init` | Initialize a Git repository |
| `git clone URL` | Clone an existing repository |

**Important flag:**
- `--global` — Apply configuration to all repositories for the current user.

## 2. Basic Git Workflow

| Command | Purpose |
|---|---|
| `git status` | Check working tree status |
| `git add file.py` | Add a file to staging |
| `git add .` | Stage changes in the current directory |
| `git add -A` | Stage all changes across the repository |
| `git commit -m "message"` | Save staged changes |
| `git commit -am "message"` | Stage and commit modified tracked files |
| `git log` | View commit history |

**Important flags:**
- `-m` — Add commit message.
- `-a` — Automatically stage modified and deleted tracked files; does not include new untracked files.

## 3. Viewing Changes

| Command | Purpose |
|---|---|
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |
| `git diff branch1 branch2` | Compare two branches |
| `git log --oneline` | Show compact commit history |
| `git log --oneline --graph --all` | View branch and commit history |
| `git show` | Show details of the latest commit |
| `git show commit_id` | Show details of a specific commit |

**Important flags:**
- `--staged` — Show changes added to staging.
- `--oneline` — Display each commit in one line.
- `--graph` — Show branch history graphically.
- `--all` — Include all branches.

## 4. Branch Management

| Command | Purpose |
|---|---|
| `git branch` | List local branches |
| `git branch branch_name` | Create a branch |
| `git switch branch_name` | Switch to a branch |
| `git switch -c branch_name` | Create and switch to a branch |
| `git branch -d branch_name` | Delete a merged branch |
| `git branch -D branch_name` | Force-delete a branch |
| `git branch -a` | List local and remote-tracking branches |

**Important flags:**
- `-c` — Create a new branch.
- `-d` — Safely delete a merged branch.
- `-D` — Force-delete a branch.

## 5. Merge and Rebase

| Command | Purpose |
|---|---|
| `git merge branch_name` | Merge another branch into the current branch |
| `git merge --abort` | Abort an ongoing merge |
| `git rebase branch_name` | Reapply current branch commits on another branch |
| `git rebase --abort` | Abort an ongoing rebase |
| `git rebase --continue` | Continue after resolving conflicts |

**Remember:**
- **Merge:** Combines branch histories and may create a merge commit.
- **Rebase:** Replays commits on top of another branch, creating new commit IDs.

## 6. Remote Repository

| Command | Purpose |
|---|---|
| `git remote -v` | Show remote repository URLs |
| `git remote add origin URL` | Add a remote repository |
| `git remote remove origin` | Remove a remote |
| `git fetch origin` | Download remote changes without merging |
| `git pull origin main` | Fetch and integrate remote changes |
| `git push origin main` | Push commits to remote |
| `git push -u origin branch_name` | Push branch and set upstream |
| `git push` | Push to configured upstream branch |

**Important flags:**
- `-v` — Show detailed remote URLs.
- `-u` — Set upstream tracking branch.

## 7. Undoing Changes

| Command | Purpose |
|---|---|
| `git restore file.py` | Discard unstaged changes in a file |
| `git restore --staged file.py` | Remove file from staging |
| `git reset --soft HEAD~1` | Undo latest commit but keep changes staged |
| `git reset HEAD~1` | Undo latest commit and keep changes unstaged |
| `git reset --hard HEAD~1` | Undo latest commit and discard its changes |
| `git revert commit_id` | Create a new commit that reverses a previous commit |

**Important flags:**
- `--soft` — Keep changes staged.
- `--mixed` — Keep changes unstaged (default).
- `--hard` — Discard changes in the working tree and staging area.

**Important:** `git reset --hard` can permanently discard uncommitted work. Use it carefully.

## 8. Stash Changes

| Command | Purpose |
|---|---|
| `git stash` | Temporarily save uncommitted changes |
| `git stash list` | List saved stashes |
| `git stash pop` | Apply latest stash and remove it |
| `git stash apply` | Apply latest stash but keep it |
| `git stash drop` | Delete latest stash |
| `git stash clear` | Delete all stashes |

**Useful flag:**
- `-u` — Include untracked files.

```bash
git stash -u
```

## 9. Other Important Commands

| Command | Purpose |
|---|---|
| `git rm file.py` | Remove file and stage its deletion |
| `git mv old.py new.py` | Rename or move a tracked file |
| `git tag` | List tags |
| `git tag v1.0` | Create a tag |
| `git tag -d v1.0` | Delete a local tag |
| `git cherry-pick commit_id` | Apply a specific commit to the current branch |
| `git blame file.py` | Show who changed each line |
| `git clean -n` | Preview untracked files to be deleted |
| `git clean -fd` | Delete untracked files and directories |

**Important flags:**
- `-n` — Dry run; show what would be deleted.
- `-f` — Force deletion.
- `-d` — Include untracked directories.

## 10. .gitignore

A `.gitignore` file specifies files and directories Git should ignore when detecting untracked changes.

Example:

```gitignore
.venv/
__pycache__/
*.pyc
.env
*.log
```

**Important:** `.gitignore` does not automatically stop tracking files that are already tracked by Git.

## 11. Important Git Concepts

| Term | Meaning |
|---|---|
| Repository | Project tracked by Git |
| Working Directory | Where you modify files |
| Staging Area | Where changes are prepared for commit |
| Commit | A saved snapshot of changes |
| Branch | Separate line of development |
| HEAD | Points to the current commit |
| Remote | Repository hosted on another server |
| Merge Conflict | Occurs when Git cannot automatically combine changes |
| `.git` | Hidden directory containing Git repository data |

## 12. Common Git Workflow

```bash
git clone URL
cd project
git switch -c feature-branch
git status
git add .
git commit -m "Add feature"
git push -u origin feature-branch
```

To update your local main branch:

```bash
git switch main
git pull origin main
```