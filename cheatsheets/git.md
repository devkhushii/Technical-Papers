# Git
## Why Git?
- Track code changes.
- Restore previous versions.
- Work with multiple developers.
- Develop features separately using branches.

## 1. Git and GitHub
-  **Version Control:** Tracks changes in files and helps restore previous versions.
- **Git:** Tracks changes in your code.
- **GitHub:** Hosts Git repositories online for collaboration.

Checks whether Git is installed.
```bash
git --version
```

Installs Git on Ubuntu.
```bash
sudo apt update && sudo apt install git
```

Sets your commit identity and displays your configuration.
```bash
git config --global user.name "Kanika"
git config --global user.email "kanika@example.com"
git config --list
```

View or edit the configuration file:
```bash
cat ~/.gitconfig
nano ~/.gitconfig
```

**GitHub setup:** Create a GitHub account and authenticate using SSH or a Personal Access Token (PAT).

---

## 2. Repository and Basic Workflow

Starts a Git repository in the current folder.
```bash
git init
```

Downloads an existing repository to your computer.
```bash
git clone https://github.com/user/project.git
```

Shows which files are changed, staged, or untracked.
```bash
git status
```

Stages a file, then saves the staged changes as a commit.
```bash
git add file.py
git commit -m "Add feature"
```
Displays a short commit history.
```bash
git log --oneline
```

#### check changes
shows changes that are not staged.
```bash
git diff
```

shows changes that are staged but not committed.
```bash
git diff --staged
```

displays details of the latest commit.
```bash
git show
```

### Git’s basic flow

```text
Working Directory  ──git add ──>  Staging Area     ── git commit ──>   Repository
    edit files                   prepare changes                     save snapshot
```

---

## 3. Connect to GitHub: Push and Pull

Connects your local repository to GitHub and displays remote URLs.
```bash
git remote add origin https://github.com/user/project.git
git remote -v
```

Uploads your commits to GitHub and sets the upstream branch.
```bash
git push -u origin main
```

Downloads and integrates changes from GitHub.
```bash
git pull origin main
```

Downloads remote updates without integrating them into your current branch.
```bash
git fetch origin
```

```text
Local Repository  ──git push──>  GitHub
Local Repository  <──git pull──  GitHub
Local Repository  <─git fetch──  GitHub (download only)
```

**Note:** `fetch` downloads; `pull` downloads and integrates; `push` uploads.

---

## 4. Branches

A branch lets you work on a feature separately from `main`.


Lists branches, then creates and switches to a new branch.
```bash
git branch
git switch -c feature-login
```

Switches back to the `main` branch.
```bash
git switch main
```

Deletes a merged branch.
```bash
git branch -d feature-login
```


```text
             feature-login
            /             \
main ──────●───────────────●──────
           start          feature
```

## `git checkout` vs `git switch`

| Command | Purpose |
|---|---|
| `git checkout branch-name` | Switch to an existing branch. |
| `git checkout -b branch-name` | Create and switch to a new branch. |
| `git checkout -- file.py` | Discard unstaged changes in a file. |
| `git switch branch-name` | Modern command to switch branches. |
| `git switch -c branch-name` | Modern command to create and switch branches. |

**Note:** `git checkout` can switch branches and restore files. Modern Git separates these tasks into `git switch` and `git restore`.


---

## 5. Merge and Pull Request

Merges `feature-login` into the current `main` branch.
```bash
git switch main
git merge feature-login
```

Cancels a merge that is in progress.
```bash
git merge --abort
```


**Merge types:**
- **Fast-forward:** Moves the branch pointer forward when possible.
- **Merge commit:** Creates a commit joining the branch histories.

```text
main:           A ── B ──────────── M
                       \           /
feature-login:          C ── D ──
                              merge
```

**Pull Request (PR):** A GitHub request to review and merge your branch into another branch.

---

## 6. Merge Conflicts

A conflict occurs when Git cannot automatically combine changes, often because the same lines were edited.


Finds files with conflicts.
```bash
git status
```

Git marks the conflicting sections in the file.
```text
<<<<<<< HEAD
Your current change
=======
Incoming change
>>>>>>> feature-login
```

After resolving the file, stages and commits the resolution.
```bash
# Edit the file and keep the correct content
git add file.py
git commit -m "Resolve merge conflict"
```


---

## 7. Fork and Pull Request

A **fork** is your own GitHub copy of someone else’s repository.


Clones your fork, creates a branch, saves your changes, and uploads the branch.
```bash
git clone https://github.com/your-user/project.git
git switch -c fix-bug
git add .
git commit -m "Fix bug"
git push -u origin fix-bug
```


```text
Original Repository
        │
      Fork
        ▼
Your GitHub Copy ──clone──> Your Computer
        │                       │
        │                   commit + push
        │                       ▼
        └──── Pull Request <── Your Branch
```

---

## 8. Undo Changes

Discards unstaged changes in a file.
```bash
git restore file.py
```

Unstages a file but keeps its changes.
```bash
git restore --staged file.py
```

Undo the latest commit while keeping changes staged.
```bash
git reset --soft HEAD~1
```

Undo the latest commit while keeping changes unstaged.
```bash
git reset HEAD~1
```

Creates a new commit that reverses an earlier commit.
```bash
git revert commit-id
```


**Note:** `git reset --hard` can permanently discard changes.

---

## 9. Important Differences

| Concept | Remember |
|---|---|
| Git vs GitHub | Version control tool vs online hosting platform |
| `add` vs `commit` | Stage changes vs save a snapshot |
| `commit` vs `push` | Save locally vs upload to remote |
| `fetch` vs `pull` | Download only vs download and integrate |
| Fork vs clone | Online copy vs local copy |
| Merge vs rebase | Join histories vs replay commits |
| Branch vs repository | Development line vs whole project |
| PR | Request to review and merge changes |

---

## 10. Diffrence between ``` git clone ```  and  ``` git remote add origin ```
| Command | Purpose |
|---|---|
| `git clone URL` | Downloads a repository and connects it to the remote. |
| `git remote add origin URL` | Connects an existing local repository to a remote. |
| `git remote -v` | Displays remote URLs. |
| `git push -u origin main` | Pushes and sets the upstream branch. |
| `git push` | Pushes to the configured upstream branch. |
| `git pull` | Fetches and integrates changes from the upstream branch. |



**Flow:** Update `main` → create branch → make changes → commit → push → open a Pull Request.