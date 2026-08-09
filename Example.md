# Git Workflow Example

This repository demonstrates a complete Git workflow followed in a real project.

---

# Repository Setup

## Clone Repository

```bash
git clone https://github.com/itsdhruvrpandey01/loanX.git
```

Move into the project.

```bash
cd loanX
```

---

# If Creating a New Repository

Initialize Git.

```bash
git init
```

Add remote repository.

```bash
git remote add origin https://github.com/itsdhruvrpandey01/loanX.git
```

Verify remote.

```bash
git remote -v
```

Output

```
origin  https://github.com/itsdhruvrpandey01/loanX.git
```

---

# Initial Commit

Check repository status.

```bash
git status
```

Stage all files.

```bash
git add .
```

Create first commit.

```bash
git commit -m "Initial setup for loanX"
```

Push to GitHub.

```bash
git push -u origin main
```

---

# Branching Strategy

Current Branch

```
main
```

Create a development branch.

```bash
git switch -c develop
```

or

```bash
git checkout -b develop
```

Check available branches.

```bash
git branch
```

Output

```
* develop
  main
```

---

# Daily Development Workflow

Modify files.

Check status.

```bash
git status
```

View changes.

```bash
git diff
```

Stage changes.

```bash
git add .
```

Commit.

```bash
git commit -m "Added application.yml configuration"
```

Push changes.

```bash
git push origin develop
```

---

# Fetch Latest Changes

Download changes from remote.

```bash
git fetch origin
```

Fetch and merge.

```bash
git pull origin develop
```

---

# View Commit History

Compact history.

```bash
git log --oneline
```

Detailed history.

```bash
git log
```

---

# Cherry Pick

Suppose a bug fix exists on develop.

```
Commit

dff40fb
```

Apply it on main.

```bash
git switch main
```

```bash
git cherry-pick dff40fb
```

Push changes.

```bash
git push origin main
```

---

# Merge

Merge develop into main.

```bash
git switch main
```

```bash
git merge develop
```

History

```
main
 \
  \
   develop
      |
      Merge
```

---

# Rebase

Instead of merge.

```bash
git switch develop
```

```bash
git rebase main
```

Before

```
A----B----C main
      \
       D----E develop
```

After

```
A----B----C main
             \
              D'----E'
```

---

# Stash

Temporarily save work.

```bash
git stash
```

View stash.

```bash
git stash list
```

Restore.

```bash
git stash pop
```

---

# Reset

Undo last commit but keep changes.

```bash
git reset --soft HEAD~1
```

Undo last commit and unstage files.

```bash
git reset HEAD~1
```

Discard everything.

```bash
git reset --hard HEAD~1
```

---

# Restore

Discard local modifications.

```bash
git restore application.yml
```

Unstage a file.

```bash
git restore --staged application.yml
```

---

# Diff Examples

Working directory vs staging area.

```bash
git diff
```

Staging area vs last commit.

```bash
git diff --staged
```

Everything vs last commit.

```bash
git diff HEAD
```

Specific file.

```bash
git diff src/main/resources/application.yml
```

Only file names.

```bash
git diff --name-only
```

Statistics.

```bash
git diff --stat
```

Compare branches.

```bash
git diff main develop
```

Compare commits.

```bash
git diff HEAD~1 HEAD
```

---

# Common Commands

| Command | Description |
|----------|-------------|
| git clone | Clone repository |
| git init | Initialize Git |
| git status | Check repository status |
| git add | Stage changes |
| git commit | Create commit |
| git log | Show commit history |
| git diff | Compare changes |
| git branch | List/Create branches |
| git switch | Switch branch |
| git checkout | Legacy switch/create branch |
| git fetch | Download remote changes |
| git pull | Fetch + Merge |
| git push | Upload commits |
| git merge | Merge branches |
| git rebase | Reapply commits |
| git cherry-pick | Copy a commit |
| git stash | Save work temporarily |
| git reset | Undo commits |
| git restore | Restore files |
| git remote | Manage remote repositories |

---

# Typical Feature Development Flow

```text
Clone Repository
        │
        ▼
git switch -c feature/login
        │
        ▼
Write Code
        │
        ▼
git status
        │
        ▼
git diff
        │
        ▼
git add .
        │
        ▼
git commit
        │
        ▼
git fetch origin
        │
        ▼
git rebase origin/main
        │
        ▼
Resolve Conflicts
        │
        ▼
git push origin feature/login
        │
        ▼
Create Pull Request
        │
        ▼
Merge into main
```

---

# Best Practices

- Commit frequently with meaningful commit messages.
- Create a new branch for every feature or bug fix.
- Pull or rebase before pushing.
- Never commit directly to `main`.
- Use `git diff` before committing.
- Use `git status` frequently.
- Keep commits small and focused.
