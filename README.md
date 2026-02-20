# 🚀 Complete Git & GitHub Tutorial: From Beginner to Advanced

Welcome! This comprehensive guide will teach you Git and GitHub from the ground up. Whether you're new to version control or looking to master advanced techniques, this tutorial has you covered.

---

## 📚 Table of Contents

1. [Introduction](#introduction)
2. [The Basics](#the-basics)
3. [Viewing History](#viewing-history)
4. [Undoing & Pausing Work](#undoing--pausing-work)
5. [Connecting to GitHub](#connecting-to-github)
6. [Branching & Merging](#branching--merging)
7. [The Open Source Workflow](#the-open-source-workflow)
8. [Pull Requests](#pull-requests)
9. [Advanced - Squashing Commits](#advanced---squashing-commits)
10. [Advanced - Merge Conflicts](#advanced---merge-conflicts)

---

## 📖 Introduction

### What's the Difference Between Git and GitHub?

**Git** is a **local version control system** that runs on your computer. It tracks changes to your files over time, allowing you to:
- Create snapshots of your project (commits)
- Undo changes if something breaks
- Work on different features simultaneously (branches)
- Collaborate by merging changes together

**GitHub** is a **cloud hosting platform** for Git repositories. It provides:
- A remote home for your Git repositories (accessible from anywhere)
- Collaboration tools (Pull Requests, Issues)
- Open-source community features (Forking, Stars)
- Backup and visibility for your code

**Think of it this way:** Git is the tool you use on your computer (like a camera), and GitHub is the photo album you upload your pictures to in the cloud (like Instagram or Google Photos).

---

## 🔧 The Basics

### Step 1: Initializing a Repository

A **repository (repo)** is a project folder that Git tracks for changes. To start using Git on a new project folder, you initialize it:

```bash
# Navigate to your project folder
cd my-project

# Initialize a new Git repository
git init
```

This creates a hidden `.git` folder that stores all version control information.

---

### Step 2: Understanding the 3 Stages of Git

Git has three main stages where your files live. Think of it like a **photography workflow**:

1. **Working Directory** 📷 — Your actual project files on disk (the "camera")
2. **Staging Area** 📦 — Files you've marked for commit (the "photo gallery for selection")
3. **Commit History** 💾 — Permanent snapshots saved in Git history (the "published album")

Here's the flow in action:

```
Working Directory  →  Staging Area  →  Commit History
   (Edit files)      (git add)        (git commit)
```

---

### Step 3: Checking Status

Use `git status` to see:
- Which files are modified
- Which files are staged
- Which files are untracked

```bash
# Check the current status of your repo
git status
```

**Example output:**
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
        script.py

nothing added to commit but untracked files present (tracking use "git add" to track)
```

---

### Step 4: Adding Files to Staging Area

To move files from the **Working Directory** to the **Staging Area**, use `git add`:

```bash
# Add a specific file
git add README.md

# Add all changed files
git add .
```

Now run `git status` again to see the files are staged (ready to commit).

---

### Step 5: Committing Your Work

A **commit** is a permanent snapshot of your project. It moves files from the **Staging Area** to the **Commit History**:

```bash
# Create a commit with a descriptive message
git commit -m "Add README and initial script"
```

**Best practices for commit messages:**
- Write in the imperative mood: "Add feature" (not "Added feature")
- Be specific: "Fix button click handler bug" (not "Fix stuff")
- Keep it concise: ~50 characters max for the subject line

---

## 📜 Viewing History

### Checking Past Commits

Use `git log` to see the history of all commits:

```bash
# View full commit history
git log
```

**Example output:**
```
commit a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6 (HEAD -> main)
Author: Your Name <your.email@example.com>
Date:   Thu Feb 20 10:30:45 2026 +0000

    Add README and initial script

commit z9y8x7w6v5u4t3s2r1q0p9o8n7m6l5k4 
Author: Your Name <your.email@example.com>
Date:   Thu Feb 20 09:15:20 2026 +0000

    Initialize project
```

**Useful `git log` variations:**

```bash
# Show a condensed one-line history
git log --oneline

# Show the last 5 commits
git log -5

# Show commits with a visual branch graph
git log --oneline --graph --all
```

---

## 🔄 Undoing & Pausing Work

### Unstaging Files

If you accidentally added a file to the staging area, you can remove it without losing the changes:

```bash
# Unstage a specific file
git restore --staged README.md

# Unstage all files
git restore --staged .
```

The file remains in your **Working Directory** with changes intact; it's just no longer staged for commit.

---

### Removing Commits

Sometimes you need to undo commits. Use `git reset` to move the HEAD pointer backward:

```bash
# Undo the last commit, but keep the changes in your working directory
git reset --soft HEAD~1

# Undo the last commit and discard all changes
git reset --hard HEAD~1

# Undo the last 3 commits but keep changes
git reset --soft HEAD~3
```

**⚠️ Warning:** `git reset --hard` permanently deletes changes. Use it carefully!

---

### Temporarily Saving Work with Stash

If you're in the middle of a feature and need to switch branches, use **stash** to temporarily save your uncommitted changes:

```bash
# Save your current work without committing
git stash

# See what you've stashed
git stash list

# Apply the most recent stash and remove it
git stash pop

# Apply a specific stash (without removing it)
git stash apply stash@{0}

# Remove a stash without applying it
git stash drop stash@{0}
```

This is perfect when you're interrupted and need to work on something urgent!

---

## 🌐 Connecting to GitHub

### Step 1: Create a Repository on GitHub

1. Go to [GitHub.com](https://github.com)
2. Click the **+** icon in the top right → **New repository**
3. Name your repo (e.g., `my-project`)
4. Choose **Public** or **Private**
5. Click **Create repository**

---

### Step 2: Add a Remote Repository

A **remote** is a link to your cloud repository. Connect your local repo to GitHub:

```bash
# Add the GitHub repo as a remote named 'origin'
# Replace <USERNAME> and <REPO-NAME> with your actual GitHub username and repo name
git remote add origin https://github.com/<USERNAME>/<REPO-NAME>.git

# Verify the remote was added
git remote -v
```

The `-v` flag shows the URLs that Git will use for fetch and push operations.

---

### Step 3: Pushing to GitHub

Move your commits from your local machine to GitHub:

```bash
# Push your local main branch to GitHub and set it as upstream
git push -u origin main

# For future pushes to the same branch, you can just use:
git push
```

The `-u` flag sets **origin main** as the upstream branch, so future `git push` commands default to this branch.

---

## 🌳 Branching & Merging

### Why Use Branches?

Branches allow you to:
- Work on features in isolation without affecting the main code
- Have multiple people work on different features simultaneously
- Keep the main branch stable and production-ready

**All branches eventually merge back into main when the feature is complete.**

---

### Creating and Switching Branches

```bash
# View all local branches
git branch

# Create a new branch
git branch feature/add-login

# Switch to a branch
git checkout feature/add-login

# Create and switch to a new branch in one command
git checkout -b feature/add-login

# Rename the current branch
git branch -m new-branch-name

# Delete a branch
git branch -d feature/add-login
```

**Naming convention:** Use descriptive names like:
- `feature/add-login`
- `bugfix/fix-email-validation`
- `docs/update-readme`

---

### Merging Branches

Once your feature is complete, merge it back into the main branch:

```bash
# Switch to the main branch first
git checkout main

# Merge your feature branch into main
git merge feature/add-login

# Delete the feature branch since it's merged
git branch -d feature/add-login

# Push the updated main branch to GitHub
git push
```

If there are no conflicting changes, Git will automatically merge the branches. (See the **Merge Conflicts** section for handling conflicts.)

---

## 👥 The Open Source Workflow

### Forking vs. Cloning: What's the Difference?

| Action | Forking | Cloning |
|--------|---------|---------|
| **What it does** | Creates YOUR OWN copy of a repo on GitHub | Downloads a copy to your local computer |
| **Ownership** | You own the forked repo | You don't own the cloned repo |
| **Use case** | Contributing to open-source projects | Working on your own repo or someone else's |
| **Upstream sync** | Available (pull from original) | Just a download |

---

### Step 1: Fork the Original Repository

On GitHub:
1. Navigate to the repository you want to contribute to
2. Click the **Fork** button in the top right
3. GitHub creates a copy under your account: `<YOUR-USERNAME>/<REPO-NAME>`

---

### Step 2: Clone Your Fork

```bash
# Clone your forked copy to your local machine
# Replace <YOUR-USERNAME> and <REPO-NAME> with your details
git clone https://github.com/<YOUR-USERNAME>/<REPO-NAME>.git

# Navigate into the repo
cd <REPO-NAME>
```

---

### Step 3: Set Upstream Remote

To stay in sync with the original repo, add it as a remote called "upstream":

```bash
# Add the original repo as upstream
# Replace <ORIGINAL-USERNAME> with the original repo owner's username
git remote add upstream https://github.com/<ORIGINAL-USERNAME>/<REPO-NAME>.git

# Verify you have both remotes
git remote -v
```

You should see:
```
origin    https://github.com/<YOUR-USERNAME>/<REPO-NAME>.git (fetch)
origin    https://github.com/<YOUR-USERNAME>/<REPO-NAME>.git (push)
upstream  https://github.com/<ORIGINAL-USERNAME>/<REPO-NAME>.git (fetch)
upstream  https://github.com/<ORIGINAL-USERNAME>/<REPO-NAME>.git (push)
```

---

### Step 4: Syncing With Upstream

Before you start work, get the latest changes from the original repo:

```bash
# Fetch updates from the original repo
git fetch upstream

# Switch to main branch
git checkout main

# Merge upstream changes into your local main
git merge upstream/main

# Push the updated main to your fork on GitHub
git push origin main
```

Now your local repo and your GitHub fork are both up-to-date with the original!

---

## 📝 Pull Requests

### The Golden Rule

**One feature/bugfix per branch, and one PR per branch.**

This keeps your contributions clean, reviewable, and easy to discuss.

### Creating a Pull Request

1. Push your feature branch to GitHub:
```bash
git push origin feature/add-login
```

2. Go to the **original repository** on GitHub (not your fork)
3. You'll see a banner suggesting to create a PR from your branch
4. Click **"Compare & pull request"**
5. Write a clear title and description:
   - **Title:** "Add login feature"
   - **Description:** Explain what the feature does, why you added it, and any relevant context
6. Click **"Create pull request"**

### Review Process

1. Maintainers review your code
2. They may request changes or approve it
3. Once approved, your PR gets merged into the main branch
4. You can delete your feature branch

---

## 🚀 Advanced - Squashing Commits

### What is Squashing?

When you're working on a feature, you might accumulate many messy commits like:
```
"Fix typo"
"Fix another typo"
"Actually now it works"
"Oops forgot semicolon"
```

**Squashing** combines all these into one clean commit:
```
"Add login feature"
```

This keeps the project history clean and readable.

---

### Interactive Rebase

Use `git rebase -i` (interactive rebase) to squash commits:

```bash
# Show the last 4 commits and allow interactive editing
git rebase -i HEAD~4
```

This opens an editor with something like:

```
pick a1b2c3d Add login form HTML
pick d4e5f6g Add login form CSS
pick g7h8i9j Add login validation
pick j0k1l2m Fix button styling
```

To squash the last 3 commits into the first one, change it to:

```
pick a1b2c3d Add login feature
squash d4e5f6g Add login form CSS
squash g7h8i9j Add login validation
squash j0k1l2m Fix button styling
```

Save and close the editor. Git will combine all four commits into one with a new message.

**Rebase options:**
- `pick` — Keep this commit as-is
- `reword` — Keep the commit but edit its message
- `squash` (or `s`) — Combine with the previous commit
- `fixup` (or `f`) — Like squash, but discard the commit message
- `drop` (or `d`) — Remove this commit entirely

---

### Pushing After Rebase

After rebasing, your local history differs from GitHub. Force-push carefully:

```bash
# Force push the rebased commits to your feature branch
git push --force-with-lease origin feature/add-login
```

**⚠️ Important:** Only use `--force-with-lease` (not `--force`). It's safer and won't accidentally overwrite others' work.

---

## ⚔️ Advanced - Merge Conflicts

### What is a Merge Conflict?

A **conflict** happens when two branches edit the same line of code differently:

```
Person A edits line 10: "console.log('Hello')"
Person B edits line 10: "console.log('Hi')"
```

Git can't automatically decide which version is correct, so it asks you to resolve it manually.

---

### Identifying Conflicts

When you try to merge and encounter a conflict:

```bash
git merge feature/add-login
```

You'll see:
```
Auto-merging script.py
CONFLICT (content): Merge conflict in script.py
Automatic merge failed; fix conflicts and then commit the result.
```

---

### Understanding Conflict Markers

Open the conflicted file and look for conflict markers:

```python
<<<<<<< HEAD
print("Hello from main")
=======
print("Hello from feature")
>>>>>>> feature/add-login
```

**The three sections:**
1. **`<<<<<<< HEAD`** — Your current branch's version (main)
2. **`=======`** — The separator
3. **`>>>>>>> feature/add-login`** — The incoming branch's version

---

### Resolving Conflicts

Manually edit the file to keep the version you want:

```python
# Option 1: Keep main's version
print("Hello from main")

# Option 2: Keep feature's version
print("Hello from feature")

# Option 3: Keep both
print("Hello from main")
print("Hello from feature")

# Option 4: Combine and refactor
print("Hello from both branches!")
```

Then remove the conflict markers entirely.

---

### Completing the Merge

```bash
# Add the resolved file
git add script.py

# Complete the merge with a commit
git commit -m "Resolve merge conflict in script.py"

# Push to GitHub
git push
```

---

### Using Merge Tools

For complex conflicts, use a visual merge tool:

```bash
# Use your configured merge tool (VS Code, Kdiff3, etc.)
git mergetool
```

This opens a graphical interface where you can click to select which version to keep.

---

## 📚 Quick Reference Cheat Sheet

```bash
# INITIALIZATION
git init                          # Initialize a new repo
git clone <url>                   # Clone an existing repo

# STATUS & HISTORY
git status                        # Show current status
git log --oneline                 # Show commit history
git diff                          # Show changes before staging

# STAGING & COMMITTING
git add <file>                    # Stage a specific file
git add .                         # Stage all changes
git commit -m "message"           # Commit staged changes
git restore --staged <file>       # Unstage a file

# UNDOING
git reset --soft HEAD~1           # Undo last commit, keep changes
git reset --hard HEAD~1           # Undo last commit, discard changes
git stash                         # Temporarily save work
git stash pop                     # Restore stashed work

# BRANCHING
git branch                        # List all branches
git branch <branch-name>          # Create a branch
git checkout <branch-name>        # Switch to a branch
git checkout -b <branch-name>     # Create and switch to a branch
git branch -d <branch-name>       # Delete a branch

# MERGING
git merge <branch-name>           # Merge a branch into current branch

# REMOTE
git remote -v                     # Show remote repositories
git remote add origin <url>       # Add a remote
git pull origin main              # Fetch and merge remote changes
git push origin main              # Push commits to remote
git push -u origin main           # Push and set upstream

# ADVANCED
git rebase -i HEAD~n              # Interactive rebase (squash commits)
git log --graph --oneline --all   # Visualize branch history
```

---

## 🎓 Learning Path Recommendation

**Day 1:** Learn The Basics → understand the 3 stages of Git

**Day 2:** Practice Viewing History and Undoing Work

**Day 3:** Connect to GitHub and push your first repo

**Day 4:** Master Branching & Merging on a practice project

**Day 5:** Fork a real open-source repo and create your first PR

**Week 2+:** Practice Squashing Commits and resolving Merge Conflicts

---

## 🤝 Tips for Success

✅ **Commit often:** Many small commits are better than one giant commit

✅ **Use descriptive messages:** Future-you will thank you-now

✅ **Test before creating a PR:** Don't make reviewers debug your code

✅ **Keep branches focused:** One feature per branch, not ten features in one branch

✅ **Review others' code:** You learn by reading good code too

✅ **Don't fear mistakes:** Git has "undo" for almost everything

---

## 🔗 Additional Resources

- [Official Git Documentation](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
- [Interactive Git Branching Game](https://learngitbranching.js.org/)

---

**Happy coding! 🎉 You now have all the tools to collaborate on projects and contribute to open source.**
