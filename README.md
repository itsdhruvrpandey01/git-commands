# Git Cheat Sheet

---

## 1. `git clone`

**Purpose:** Copy an existing remote repository to your local machine.

```bash
git clone https://github.com/dhruv/los-project.git
```

Result:

```
los-project/
    .git/
    src/
    pom.xml
```

---

## 2. `git init`

**Purpose:** Initialize a new Git repository.

```bash
mkdir DemoProject
cd DemoProject
git init
```

Result:

```
Initialized empty Git repository
```

---

## 3. `git status`

**Purpose:** Check the current state of your repository.

```bash
git status
```

Example Output:

```
On branch feature/login

Modified:
    UserService.java

Untracked:
    LoginController.java
```

---

## 4. `git add`

**Purpose:** Move changes to the staging area.

```bash
git add UserService.java
```

Or stage everything:

```bash
git add .
```

---

## 5. `git commit`

**Purpose:** Save staged changes as a snapshot.

```bash
git commit -m "Added login validation"
```

Creates a new commit.

---

## 6. `git log`

**Purpose:** View commit history.

```bash
git log --oneline
```

Output:

```
8ab12f2 Added login validation
6fd22ce Fixed API bug
4ac98fe Initial commit
```

I would only enhance the **`git diff`** section, since that's where the extra variants belong.

Replace your current **Section 7** with this:

---

## 7. `git diff`

**Purpose:** Compare changes between the Working Directory, Staging Area, Commits, or Branches.

### Compare unstaged changes (Working Directory ↔ Staging Area)

```bash
git diff
```

Output:

```diff
- return false;
+ return true;
```

---

### Compare staged changes (Staging Area ↔ Last Commit)

```bash
git diff --staged
```

or

```bash
git diff --cached
```

---

### Compare everything with the last commit

```bash
git diff HEAD
```

---

### Compare a specific file

```bash
git diff UserService.java
```

---

### Show only the names of changed files

```bash
git diff --name-only
```

Output:

```
UserService.java
LoginController.java
pom.xml
```

---

### Show file change statistics

```bash
git diff --stat
```

Output:

```
UserService.java     | 12 +++++++-----
LoginController.java |  8 ++++++++
pom.xml              |  2 +-
```

---

### Compare two branches

```bash
git diff main feature/login
```

---

### Compare two commits

```bash
git diff ab12345 cd45678
```

---

### Compare current branch with remote main

```bash
git diff origin/main
```

---

### Compare previous commit with current commit

```bash
git diff HEAD~1 HEAD
```

---

### **Quick Revision**

| Command                    | Compares                                       |
| -------------------------- | ---------------------------------------------- |
| `git diff`                 | Working Directory ↔ Staging Area               |
| `git diff --staged`        | Staging Area ↔ Last Commit (HEAD)              |
| `git diff HEAD`            | Working Directory + Staging Area ↔ Last Commit |
| `git diff file.java`       | Changes in one file                            |
| `git diff --name-only`     | Names of changed files only                    |
| `git diff --stat`          | File change summary                            |
| `git diff branch1 branch2` | Two branches                                   |
| `git diff commit1 commit2` | Two commits                                    |
| `git diff origin/main`     | Local branch vs remote main                    |
| `git diff HEAD~1 HEAD`     | Previous commit vs current commit              |

---


## 8. `git branch`

**Purpose:** List or create branches.

List branches:

```bash
git branch
```

Output:

```
main
* feature/login
```

Create a new branch:

```bash
git branch feature/payment
```

---

## 9. `git switch`

**Purpose:** Switch branches (modern command).

```bash
git switch feature/payment
```

Create and switch:

```bash
git switch -c feature/payment
```

---

## 10. `git checkout`

**Purpose:** Older command used for switching branches or restoring files.

Switch branch:

```bash
git checkout main
```

Create and switch:

```bash
git checkout -b feature/profile
```

---

## 11. `git fetch`

**Purpose:** Download remote changes without merging.

```bash
git fetch origin
```

Now your local repository knows about remote updates, but your branch is unchanged.

---

## 12. `git pull`

**Purpose:** Fetch and merge remote changes.

```bash
git pull origin main
```

Equivalent to:

```text
git fetch
git merge
```

---

## 13. `git push`

**Purpose:** Upload commits to the remote repository.

```bash
git push origin feature/login
```

---

## 14. `git merge`

**Purpose:** Merge another branch into the current branch.

Current branch:

```
main
```

Merge feature:

```bash
git merge feature/login
```

History:

```
main
   \
    feature/login
        |
        Merge
```

---

## 15. `git rebase`

**Purpose:** Replay commits on top of another branch to create a cleaner history.

```bash
git switch feature/login
git rebase main
```

Before:

```
A---B---C main
     \
      D---E feature
```

After:

```
A---B---C main
         \
          D'---E'
```

---

## 16. `git cherry-pick`

**Purpose:** Copy a specific commit from another branch.

Commit:

```
ab12345 Fixed login bug
```

Apply it:

```bash
git cherry-pick ab12345
```

Only that commit is copied.

---

## 17. `git stash`

**Purpose:** Temporarily save uncommitted changes.

Save work:

```bash
git stash
```

Later restore:

```bash
git stash pop
```

Useful when:

```
Working...
↓

Boss: "Fix production bug"

↓

git stash
git switch main
```

---

## 18. `git reset`

**Purpose:** Move `HEAD` and optionally unstage or discard commits.

### Soft (keep staged changes)

```bash
git reset --soft HEAD~1
```

### Mixed (default, keep working directory changes)

```bash
git reset HEAD~1
```

### Hard (discard everything)

```bash
git reset --hard HEAD~1
```

---

## 19. `git restore`

**Purpose:** Undo file changes without affecting commit history.

Restore file:

```bash
git restore UserService.java
```

Unstage a file:

```bash
git restore --staged UserService.java
```

---

## 20. `git remote`

**Purpose:** Manage remote repositories.

View remotes:

```bash
git remote -v
```

Output:

```
origin  https://github.com/dhruv/project.git
```

Add a remote:

```bash
git remote add origin https://github.com/dhruv/project.git
```

---

# Typical Daily Workflow

```text
1. git clone <repo>

2. git switch -c feature/login

3. Make code changes

4. git status

5. git add .

6. git commit -m "Implemented login API"

7. git fetch origin

8. git rebase origin/main
   (or git pull origin main)

9. Resolve conflicts (if any)

10. git push origin feature/login

11. Create Pull Request

12. After approval:
    git switch main
    git pull origin main
```

---

# Interview Quick Revision Table

| Command           | Purpose                       | Example                   |
| ----------------- | ----------------------------- | ------------------------- |
| `git clone`       | Copy remote repo              | `git clone <url>`         |
| `git init`        | Initialize Git                | `git init`                |
| `git status`      | Check repository state        | `git status`              |
| `git add`         | Stage changes                 | `git add .`               |
| `git commit`      | Save staged snapshot          | `git commit -m "msg"`     |
| `git log`         | View history                  | `git log --oneline`       |
| `git diff`        | Show code changes             | `git diff`                |
| `git branch`      | List/create branches          | `git branch feature`      |
| `git switch`      | Switch branches               | `git switch main`         |
| `git checkout`    | Switch/create branch (legacy) | `git checkout -b feature` |
| `git fetch`       | Download remote updates       | `git fetch origin`        |
| `git pull`        | Fetch + merge                 | `git pull origin main`    |
| `git push`        | Upload commits                | `git push origin feature` |
| `git merge`       | Combine branches              | `git merge feature`       |
| `git rebase`      | Replay commits on new base    | `git rebase main`         |
| `git cherry-pick` | Copy one commit               | `git cherry-pick <hash>`  |
| `git stash`       | Temporarily save changes      | `git stash`               |
| `git reset`       | Move `HEAD` / undo commits    | `git reset --soft HEAD~1` |
| `git restore`     | Discard or unstage changes    | `git restore file.java`   |
| `git remote`      | Manage remotes                | `git remote -v`           |
| `git diff`             | Compare code changes                    | `git diff`             |
| `git diff --staged`    | Compare staged changes with last commit | `git diff --staged`    |
| `git diff --name-only` | Show only changed file names            | `git diff --name-only` |
| `git diff --stat`      | Show change summary                     | `git diff --stat`      |
