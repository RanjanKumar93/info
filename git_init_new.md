### Step 1: Initialize Git in Your Project Directory

Navigate to your project directory (if you haven't already), and initialize Git:

```bash
git init
```

### Step 2: Add All Files and Commit

Add all the files in your project directory to the Git repository and commit them:

```bash
git add .
git commit -m "Initial commit"
```

### Step 3: Create a New Repository on GitHub

1. Go to [GitHub](https://github.com) and log in to your account.
2. Click on the **+** icon in the top right corner and select **New repository**.
3. Give your repository a name (e.g., `flutter_crud_app`), add a description if you'd like, and choose whether it should be public or private.
4. **Do not initialize the repository with a README, .gitignore, or license**, as you’ve already initialized the Git repository locally.
5. Click **Create repository**.

### Step 4: Add the GitHub Repository as a Remote

After creating the repository on GitHub, you will be provided with a repository URL. Add it as a remote to your local Git repository. Replace `YOUR_USERNAME` and `YOUR_REPOSITORY_NAME` with your GitHub username and repository name:

```bash
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY_NAME.git
```

### Step 5: Push Your Code to GitHub

Push your local commits to the GitHub repository:

```bash
git branch -M main
git push -u origin main
```

### Step 6: Verify Your Repository on GitHub

Go back to your GitHub repository page and refresh it. You should now see your Flutter project files uploaded to the repository.

### Optional: Add a `.gitignore` for Flutter

To prevent unnecessary files from being tracked by Git (e.g., build files, local configurations), it's a good idea to add a `.gitignore` file tailored for Flutter. You can do this by creating a `.gitignore` file in your project root with the following content:

```plaintext
# Flutter/Dart/Pub related
.dart_tool/
.packages
build/
flutter_*.yaml

# Dependency directories
ios/Pods/
linux/flutter/ephemeral/
windows/flutter/ephemeral/
macos/Pods/
web/.dart_tool/

# Generated files
*.iml
*.ipr
*.iws
.idea/

# Android/IntelliJ
*.apk
*.aar
*.lock

# iOS/Xcode
DerivedData/
*.xcuserdatad/
*.hmap
*.ipa

# VS Code
.vscode/
```

Then, add it to Git and commit:

```bash
git add .gitignore
git commit -m "Add .gitignore"
git push
```
