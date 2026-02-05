# 🐙 Git Master Cheat Sheet

Welcome to your ultimate guide to Git! This cheat sheet covers the essential commands you'll use daily, plus advanced workflows for team collaboration.

---

## ⚙️ 1. Configuration

Set up your identity. You only need to do this once per machine.

| Command                                            | Description                              |
| -------------------------------------------------- | ---------------------------------------- |
| `git config --global user.name "Your Name"`        | Set your username                        |
| `git config --global user.email "you@example.com"` | Set your email (must match GitHub email) |
| `git config --list`                                | View your current configuration          |
| `git config --global core.editor "code --wait"`    | Set VS Code as default editor            |
| `git config --global core.editor "cursor --wait"`  | Set Cursor as default editor             |

---

## 🚀 2. Starting a Project

| Command           | Description                                           |
| ----------------- | ----------------------------------------------------- |
| `git init`        | Initialize a new git repository in the current folder |
| `git clone <url>` | Clone (download) an existing repository from GitHub   |

---

## 🙈 3. Ignoring Files (.gitignore)

Create a file named `.gitignore` in your root directory to specify files Git should **ignore** (not track).

**Common files to ignore:**

- `node_modules/` (Heavy dependencies)
- `.env` (API keys & secrets - **NEVER PUSH THIS**)
- `.DS_Store` (Mac system file)
- `dist/` or `build/` (Compiled code)

| Command                  | Description                                                                                    |
| ------------------------ | ---------------------------------------------------------------------------------------------- |
| `touch .gitignore`       | Create the ignore file                                                                         |
| `git rm --cached <file>` | Stop tracking a file but keep it on your disk (useful if you accidentally committed env files) |

---

## 📸 4. The Daily Workflow (Stage & Commit)

| Command                        | Description                                        |
| ------------------------------ | -------------------------------------------------- |
| `git status`                   | **ALWAYS RUN THIS.** check what files have changed |
| `git add <filename>`           | Stage a specific file                              |
| `git add .`                    | Stage **all** changes (new, modified, deleted)     |
| `git commit -m "Your message"` | Commit staged changes with a descriptive message   |
| `git diff`                     | Show unstaged file changes                         |

---

## 🌿 5. Branching

Never work on `main` directly! Use branches for features.

| Command                         | Description                                         |
| ------------------------------- | --------------------------------------------------- |
| `git branch`                    | List all local branches                             |
| `git branch <branch-name>`      | Create a new branch                                 |
| `git switch <branch-name>`      | Switch to a specific branch                         |
| `git switch -c <branch-name>`   | Create **AND** switch to a new branch (Modern way)  |
| `git checkout -b <branch-name>` | Create **AND** switch to a new branch (Classic way) |
| `git merge <branch-name>`       | Merge `<branch-name>` _into_ your current branch    |
| `git branch -d <branch-name>`   | Delete a branch (after merging)                     |
| `git branch -D <branch-name>`   | Force delete a branch (unmerged changes)            |

---

## ☁️ 6. Remote (GitHub)

Interacting with the cloud (GitHub/GitLab).

| Command                               | Description                                           |
| ------------------------------------- | ----------------------------------------------------- |
| `git remote add origin <url>`         | Link local repo to a remote GitHub repo               |
| `git remote -v`                       | Verify remote connections (view URLs)                 |
| `git remote set-url origin <new-url>` | Change the URL of the remote (e.g., switching to SSH) |
| `git remote remove origin`            | Remove the link to the remote repository              |
| `git push -u origin <branch>`         | Push branch to GitHub (first time)                    |
| `git push`                            | Push changes to GitHub (after linking)                |
| `git pull origin <branch>`            | Pull latest changes from GitHub to local              |
| `git fetch`                           | Download info about remote branches (doesn't merge)   |

---

## 🤝 7. Collaboration Workflow (Team Projects)

When working with a team, follow this cycle to avoid conflicts:

1.  **Sync First**: Always pull the latest code before starting work.
    ```bash
    git checkout main
    git pull origin main
    ```
2.  **Create Branch**: Create a branch for your feature.
    ```bash
    git switch -c feature-login-page
    ```
3.  **Work & Commit**: Code, stage, and commit often.
    ```bash
    git add .
    git commit -m "Build login form layout"
    ```
4.  **Push**: Send your branch to GitHub.
    ```bash
    git push -u origin feature-login-page
    ```
5.  **Pull Request (PR)**: Go to GitHub and open a Pull Request to merge into `main`.

---

## ↩️ 8. Undoing Mistakes

| Command                    | Description                                                                 |
| -------------------------- | --------------------------------------------------------------------------- |
| `git checkout -- <file>`   | Discard changes in a file (revert to last commit)                           |
| `git restore <file>`       | Modern way to discard changes in a file                                     |
| `git reset HEAD <file>`    | Unstage a file (remove from staging area)                                   |
| `git reset --soft HEAD~1`  | Undo last commit but keep changes staged (fix typo in commit)               |
| `git reset --hard HEAD~1`  | **DANGER**: Undo last commit & **DELETE** changes                           |
| `git revert <commit-hash>` | Create a _new_ commit that undoes a previous commit (Safe for shared repos) |

### 🚨 EMERGENCY: I pushed a `.env` file!

**First:** Rotate/Change your API keys immediately. Bots scrape GitHub in seconds.
**Second:** To scrub it from **all** commit history (Nuclear option):

```bash
git filter-branch --index-filter "git rm -rf --cached --ignore-unmatch .env" HEAD
git push --force
```

_Warning: This rewrites history. If working in a team, everyone else will need to re-clone the repo._

---

## 📦 9. Stashing

Save work temporarily without committing to switch branches.

| Command           | Description                              |
| ----------------- | ---------------------------------------- |
| `git stash`       | Save uncommitted changes temporarily     |
| `git stash pop`   | Apply saved changes back and clear stash |
| `git stash list`  | See list of stashed changes              |
| `git stash clear` | Delete all stashed changes               |

---

## 📜 10. View History

| Command                           | Description              |
| --------------------------------- | ------------------------ |
| `git log`                         | View commit history      |
| `git log --oneline`               | View compact history     |
| `git log --oneline --graph --all` | View pretty commit graph |

---

## 💡 Pro Tips for Bootcamp Success

1. **Commit often**: Small commits are easier to fix than huge ones.
2. **Descriptive Messages**: Use "Fix login bug" instead of "update".
3. **Always Pull before Push**: When working in teams, sync first!
4. **Protect Secrets**: Never push `.env` files. If you did, rename the variable and rotate the key immediately.

HAPPY CODING! 👩‍💻👨‍💻
