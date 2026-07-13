# Software Essentials — Quick Recall

## 01. Master Git & GitHub in One Video! 🚀 Level Up Your Skills Now!

**Video:** [Master Git & GitHub in One Video!](https://youtu.be/AB3J8ufDYHQ?si=kQDCDTyTnPhct0yF) · **Date:** July 13, 2026
→ Deep-dive: [01-git-and-github.md](01-git-and-github.md)

### TL;DR
A comprehensive guide to local version control with Git and online repository hosting with GitHub, covering lifecycle commands, branching, stashing, tagging, rebasing, and collaboration.

### Key Points
* **Git vs. GitHub** — Git is a local command-line version control engine, while GitHub is a cloud-based hosting platform for remote Git repositories.
* **Under the Hood Areas** — Git manages changes through the Working Directory (modified files), Staging Area (queued snapshot index), Local Repository (committed database), and Remote Repository (shared online server).
* **The Stash Stack** — Git Stash shelves uncommitted workspace modifications temporarily, allowing developers to switch branches without prematurely committing raw code.
* **The Golden Rule of Rebasing** — Rebase rewrites history; never rebase commits that have been pushed to a public/shared remote repository, or you will break colleagues' sync state.
* **Merge Conflicts** — Occur when overlapping lines are edited concurrently; resolved by manually stripping the conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) and staging the files.
* **Convention Over Config** — Empty directories are not tracked by Git; use an empty `.gitkeep` placeholder file inside the directory to force folder tracking.

### Terms Introduced
| Term | Definition (one line) |
|---|---|
| **VCS** | Version Control System — software that tracks historical modifications to directories. |
| **DVCS** | Distributed VCS — a VCS where every workstation holds a complete repository copy (e.g., Git). |
| **Merge Commit** | A commit created automatically when combining two divergent branches via a 3-way merge. |
| **Git Stash** | A stack-based temporary storage area for holding uncommitted modifications. |
| **Squashing** | The process of combining multiple local commits into a single commit during interactive rebase. |
| **SemVer** | Semantic Versioning — a major.minor.patch version numbering scheme for releases. |

### Self-Test
- Why does Git completely ignore empty folders, and how can you circumvent this limit?
- What is the difference between `git pull` and `git fetch`?
- Write a sequence of commands to resolve a merge conflict in a file named `main.py` after a failed `git merge feature-a` operation.
