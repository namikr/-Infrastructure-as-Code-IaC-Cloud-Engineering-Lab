# 🧪 Lab 01 — Git Fundamentals

### Version Control, Branching, Collaboration & Change History

**Foundation Series**

![Git](https://img.shields.io/badge/Git-Version_Control-F05032?logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-Collaboration-181717?logo=github&logoColor=white)
![Difficulty](https://img.shields.io/badge/Difficulty-Beginner-success)
![Status](https://img.shields.io/badge/Status-In_Progress-yellow)

---

## 🎯 Lab Overview

Git is a distributed version control system that helps engineers track changes, manage source code, collaborate, and maintain a reliable history of their work.

In modern DevOps environments, Git is a foundation for Infrastructure as Code (IaC), CI/CD pipelines, configuration management, and application development.

This lab introduces essential Git workflows used in real-world engineering environments.

**Objective:** Build a small project, manage changes through branches, submit a Pull Request, merge changes, and inspect the project's history.

## 📚 Learning Objectives

By completing this lab, you will learn how to:

- Initialize and configure a local Git repository.
- Track files and manage changes.
- Create meaningful commits.
- Create and switch between branches.
- Push changes to GitHub.
- Create and review Pull Requests.
- Merge branches.
- Compare changes and inspect commit history.
- Revert unwanted changes safely.

## 🛠️ Prerequisites

| Requirement | Description |
|---|---|
| Git | Installed locally |
| GitHub | GitHub account |
| Terminal | PowerShell, Bash, or Git Bash |
| Code editor | VS Code recommended |

Useful resources:

- [Git official documentation](https://git-scm.com/doc)
- [GitHub documentation](https://docs.github.com/)
- [GitHub Skills](https://skills.github.com/)

---

## 🏗️ Part 1 — Initialize a Repository

### Step 1: Configure Git

Set the name and email associated with your commits:

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Verify the configuration:

```bash
git config --list
```

### Step 2: Create the project

```bash
mkdir git-fundamentals-lab
cd git-fundamentals-lab
```

Initialize the repository:

```bash
git init
```

Check its status:

```bash
git status
```

**Expected result:** Git initializes an empty repository and reports that there are no commits yet.

### Step 3: Create project files

Create these files:

```text
git-fundamentals-lab/
├── README.md
├── project-overview.md
└── deployment-notes.md
```

Add this content to `README.md`:

```markdown
# Git Fundamentals Lab

This project demonstrates essential Git workflows.

## Topics

- Repository initialization
- Branching
- Commits
- Pull Requests
- Change history
```

### Step 4: Stage and commit

Add the files to the staging area:

```bash
git add .
```

Create the first commit:

```bash
git commit -m "Initial commit: create Git fundamentals project"
```

View the history:

```bash
git log --oneline
```

**Engineering concept:** A commit records a snapshot of the project, along with an identifier and metadata.

---

## 🌿 Part 2 — Branching & Collaboration

Branches let engineers develop features or fix issues independently without immediately changing the main codebase.

### Step 1: Create a feature branch

```bash
git switch -c feature/project-overview
```

Verify the active branch:

```bash
git branch
```

### Step 2: Make changes

Open `project-overview.md` and add:

```markdown
# Project Overview

This lab demonstrates how Git supports:

- Version control
- Collaborative development
- Change tracking
- Infrastructure automation
- CI/CD workflows
```

Stage and commit the change:

```bash
git add project-overview.md
git commit -m "Add project overview and learning objectives"
```

### Step 3: Create a GitHub repository and push the branch

On GitHub, create a repository named `git-fundamentals-lab`. If you already have a local project, create the GitHub repository without initializing it with another README, license, or `.gitignore`.

Connect your local repository (replace `YOURUSERNAME` with your GitHub username):

```bash
git remote add origin https://github.com/YOURUSERNAME/git-fundamentals-lab.git
```

If your default branch is not already named `main`, rename it:

```bash
git branch -M main
```

Push `main` first if it has not yet been published:

```bash
git switch main
git push -u origin main
```

Then push your feature branch:

```bash
git switch feature/project-overview
git push -u origin feature/project-overview
```

**Expected result:** Your local project and feature branch are available on GitHub.

---

## 🔀 Part 3 — Pull Requests

A Pull Request (PR) lets engineers propose changes and request review before merging them into the main branch.

### Step 1: Open a Pull Request

1. Navigate to your GitHub repository.
2. Open the **Pull requests** tab.
3. Select **New pull request**.
4. Set the base branch to `main`.
5. Set the compare branch to `feature/project-overview`.

### Step 2: Create the Pull Request

**Title:**

`Add project overview documentation`

**Description:**

```markdown
## Summary

Adds project overview documentation to the Git Fundamentals Lab.

## Changes

- Added project objectives
- Documented key Git concepts
- Introduced the project structure

## Testing

- Verified Markdown formatting
- Reviewed changes before merging

## Review

Ready for review and merge.
```

### Step 3: Review the changes

Before merging, examine:

- Files changed.
- Lines added or removed.
- Commit history.
- Potential mistakes.
- Documentation quality.

### Step 4: Merge the Pull Request

For this exercise, select **Merge pull request**, then **Confirm merge**.

Update your local `main` branch:

```bash
git switch main
git pull origin main
```

Your feature branch changes are now included in the local `main` branch.

---

## 📜 Part 4 — Change History & Version Tracking

Understanding Git history is useful when troubleshooting infrastructure changes or investigating unexpected behavior.

### Essential Git commands

| Command | Purpose |
|---|---|
| `git status` | Check the working tree |
| `git log` | View commit history |
| `git log --oneline` | View compact commit history |
| `git log --oneline --graph --all` | Visualize branches and commits |
| `git show` | Inspect a commit |
| `git diff` | Compare working changes |
| `git diff main..branch` | Compare two branches |
| `git branch -a` | List local and remote branches |
| `git remote -v` | View remote repositories |
| `git blame README.md` | See who last changed each line |

### Exercise: Inspect your history

```bash
git log --oneline --graph --all
```

Inspect the latest commit:

```bash
git show HEAD
```

Check uncommitted changes:

```bash
git diff
```

### Exercise: Revert a change

Make an intentional test change in `deployment-notes.md`, then commit it:

```bash
git add deployment-notes.md
git commit -m "Add test deployment notes"
```

Find the commit:

```bash
git log --oneline
```

Revert the latest commit:

```bash
git revert HEAD
```

Inspect the history again:

```bash
git log --oneline
```

**Important:** `git revert` creates a new commit that reverses the changes introduced by an earlier commit. It preserves existing history and is generally safer for shared branches than rewriting history.

---

## 🧠 Part 5 — Engineering Best Practices

Good Git practices make collaboration safer and projects easier to maintain.

### Commit message conventions

Use clear, descriptive messages. One useful convention is:

| Type | Example |
|---|---|
| `feat` | `feat: add AWS VPC module` |
| `fix` | `fix: correct subnet configuration` |
| `docs` | `docs: update deployment guide` |
| `refactor` | `refactor: simplify Terraform variables` |
| `test` | `test: add infrastructure validation` |
| `chore` | `chore: update project dependencies` |

### Recommended branching strategy

```text
main
 ├── feature/new-feature
 │    └── Commit changes
 ├── feature/security-update
 │    └── Commit changes
 └── bugfix/configuration-error
      └── Commit changes
```

Recommended practices:

- Keep `main` stable.
- Create a branch for each feature or bug fix.
- Commit small, logical changes.
- Review Pull Requests before merging.
- Never commit credentials, passwords, or API keys.
- Use `.gitignore` to exclude temporary files and sensitive local configuration.
- Protect important branches with GitHub branch protection rules.

---

## 🧩 Part 6 — Practical Challenge

Complete this challenge using the skills from the earlier sections.

1. Create a new Git repository.
2. Add a README and two Markdown files.
3. Commit the initial project.
4. Create a branch called `feature/deployment-guide`.
5. Add deployment instructions.
6. Push the branch to GitHub.
7. Open a Pull Request.
8. Review and merge the changes.
9. Inspect the commit history.
10. Revert one test commit.

### ⭐ Bonus Challenge

- Create a `.gitignore` file.
- Configure branch protection for `main`.
- Explore how Git can become the foundation for an automated CI/CD pipeline.

---

## 🏁 Lab Completion Checklist

- [ ] Installed and configured Git.
- [ ] Initialized a repository.
- [ ] Created project files.
- [ ] Staged and committed changes.
- [ ] Created and switched branches.
- [ ] Connected to GitHub.
- [ ] Pushed a feature branch.
- [ ] Created a Pull Request.
- [ ] Reviewed and merged changes.
- [ ] Inspected commit history.
- [ ] Compared changes using `git diff`.
- [ ] Successfully reverted a commit.
- [ ] Completed the bonus challenge.

## 📸 Evidence of Completion

Capture screenshots showing:

1. Your initialized repository.
2. Your branch structure.
3. Your commit history.
4. Your GitHub Pull Request.
5. Your merged Pull Request.
6. Your final repository history.

Store them in the `screenshots/` folder.

---

## 🎓 Key Takeaways

Git is more than a source code management tool. It provides the foundation for controlled, collaborative, and repeatable engineering workflows.

In Infrastructure as Code environments, Git allows infrastructure definitions to be version controlled, reviewed, tested, and integrated into automated deployment pipelines.

**Next Lab:** Lab 02 — Terraform Fundamentals: Provisioning Your First Cloud Infrastructure.

---

[⬆ Back to Lab Index](../../README.md)
