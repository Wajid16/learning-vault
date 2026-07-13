# Software Essentials

> Core software engineering tooling, version control, and collaboration workflows essential for modern AI engineers.

## Progress

| # | Title | Summary | Long Note | Quick Recall |
|---|---|---|---|---|
| 01 | Git & GitHub | Complete Git lifecycle, VCS concepts, branching, stashing, rebasing, tags, GitHub integration, conflicts, multi-user collaboration, and modern workflows | [01-git-and-github.md](notes/01-git-and-github.md) | [Quick Recall Card](notes/quick-recall.md#01-git-and-github) |

## Course Outline

This course covers foundational software development essentials, starting with version control:

1. **Version Control Fundamentals**
   - Version Control Systems (VCS) & History (Linus Torvalds, April 2005)
   - Centralized vs. Distributed VCS
   - Git vs. GitHub (Tool vs. Hosting Platform)
2. **Git Mechanics & Architecture**
   - Under the Hood: Working Directory, Staging Area, Local Repository, Remote Repository
   - The `.git` internal configuration database folder
3. **Hands-on Git Basics**
   - Configuration (`git config --global user.name` / `user.email`)
   - Repository initialization (`git init`)
   - Tracking states (`git status`, `git add`, `git commit`)
   - Commit history inspection (`git log`, `git log --oneline`)
   - Discarding changes (`git restore --staged`)
4. **Intermediate Workflows**
   - Ignoring files (`.gitignore` patterns, env files, build directories)
   - Tracking empty folders (`.gitkeep`)
   - Branching & Head pointer mechanics (`git branch`, `git switch`)
   - Merge operations and resolving merge conflicts in VS Code
5. **Advanced Git Mechanics**
   - Git Stashing (`git stash`, `pop`, `apply`, `list`, `clear`, `drop`)
   - Git Tags (semantic versioning, lightweight vs. annotated)
   - Git Rebasing (`git rebase` vs. `git merge`, interactive rebase & squashing)
6. **Remote Collaboration & Platforms**
   - SSH Key Authentication (`ssh-keygen`, profile management)
   - Remote repositories (`git remote`, `git push`, `git pull`, `git fetch`)
   - GitHub Desktop GUI & VS Code Git Integration
   - Multi-User Workflow: branching, Pull Requests (PRs), code reviews, and remote merging
7. **Modern Best Practices**
   - Conventional Commits structure
   - Branch naming conventions
   - Trunk-based development vs. Git Flow
