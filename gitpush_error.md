This error occurs because the remote repository has changes that your local repository doesn't have. To resolve this, you'll need to pull the latest changes from the remote repository, merge them with your local changes, and then push the combined result.

Here's how you can do it:

### 1. **Pull the Latest Changes from the Remote Repository**
   
   Run the following command to fetch and merge the changes from the remote `main` branch:

   ```bash
   git pull origin main
   ```

   This command will:
   - Fetch the latest changes from the remote repository.
   - Attempt to merge those changes with your local branch.

   If there are no conflicts, the merge will succeed, and you can proceed to push your changes.

### 2. **Resolve Merge Conflicts (If Any)**
   
   If there are any conflicts between your local changes and the remote changes, Git will notify you. You'll need to manually resolve these conflicts:

   - Open the files with conflicts and decide how to merge the changes.
   - After resolving conflicts, mark the files as resolved:

     ```bash
     git add <filename>
     ```

   - Complete the merge:

     ```bash
     git commit -m "Resolved merge conflicts"
     ```

### 3. **Push Your Changes**
   
   Once the pull and any necessary conflict resolution are done, push your changes to the remote repository:

   ```bash
   git push origin main
   ```

### 4. **Force Push (Only if Necessary)**
   
   If you don't want to merge the remote changes and are sure your local changes should overwrite the remote, you can force push:

   ```bash
   git push origin main --force
   ```

   **Note:** Force pushing will overwrite the remote branch with your local branch, potentially deleting changes made by others. Use this with caution.

### Summary
1. **Pull**: `git pull origin main`
2. **Resolve conflicts** (if any).
3. **Push**: `git push origin main`
4. **Force push** (only if necessary): `git push origin main --force`

This should resolve the issue and allow you to push your changes successfully.