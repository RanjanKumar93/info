# Git

### **Ch 1. Setup**
- **Install Git**: Available for Windows, macOS, and Linux.
- **Configuration**: Use `git config --global` to set user information, e.g., `git config --global user.name "Your Name"` and `git config --global user.email "your.email@example.com"`.
- **Check Version**: `git --version`.

### **Ch 2. Repositories**
- **Initialize a Repo**: `git init` creates a new repository.
- **Clone a Repo**: `git clone <url>` copies a remote repository to your local machine.
- **Status**: `git status` shows the current state of the working directory and staging area.

### **Ch 3. Internals**
- **Commit Structure**: Git stores snapshots of your project in the form of commits.
- **Objects**: Git uses blobs (file contents), trees (directory structure), and commits (history) to track changes.
- **Branches**: Pointers to commits, allowing parallel development.

### **Ch 4. Config**
- **User Settings**: Global vs. local config (e.g., `~/.gitconfig` for global and `.git/config` for local).
- **Aliases**: Define shortcuts for commands (e.g., `git config --global alias.co checkout`).
- **File Format**: INI-style format with sections, keys, and values.

### **Ch 5. Branching**
- **Create a Branch**: `git branch <branch-name>` creates a new branch.
- **Switch Branch**: `git checkout <branch-name>` moves to the branch.
- **View Branches**: `git branch` lists all branches.

### **Ch 6. Merge**
- **Fast-Forward Merge**: Happens when there is a linear path between branches.
- **Three-Way Merge**: Combines branches with diverged history.
- **Resolve Conflicts**: Occur when changes overlap; requires manual fixing.

### **Ch 7. Rebase**
- **Linear History**: Reapplies commits from one branch onto another.
- **Interactive Rebase**: Use `git rebase -i` to reorder, squash, or edit commits.
- **Rebase vs. Merge**: Rebase changes history, merge preserves history.

### **Ch 8. Reset**
- **Soft Reset**: Moves HEAD to a previous commit, but keeps changes in the working directory and staging area (`git reset --soft <commit>`).
- **Mixed Reset**: Resets the staging area but keeps working directory changes (`git reset --mixed <commit>`).
- **Hard Reset**: Resets everything, including the working directory (`git reset --hard <commit>`).

### **Ch 9. Remote**
- **Add a Remote**: `git remote add <name> <url>` links a local repo to a remote.
- **Fetch**: `git fetch <remote>` retrieves updates from the remote without merging.
- **Push/Pull**: `git push <remote> <branch>` pushes local changes; `git pull` fetches and merges remote changes.

### **Ch 10. GitHub**
- **Create a Repository**: Use GitHub to host repositories.
- **Fork**: Create a personal copy of another user’s repository.
- **Pull Request**: Propose changes to a repository.
- **Issues**: Track tasks, bugs, or features.

### **Ch 11. Gitignore**
- **Purpose**: Specifies files that Git should ignore (e.g., temporary files, logs).
- **File Structure**: Use wildcard patterns to define ignored files (e.g., `*.log` for all log files).
- **Global Gitignore**: Set up a global `.gitignore` file for patterns across all repositories.
