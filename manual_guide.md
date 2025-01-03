# Step-by-Step Guide: Setting Up VS Code, Git, and GitHub SSH Key

## 1. Download and Install VS Code and Git Bash
- Download **VS Code** from [Visual Studio Code Official Website](https://code.visualstudio.com/).
- Run the installer and follow the setup wizard. Ensure the option to **Add VS Code to PATH** is checked.
- Download **Git** from [Git Official Website](https://git-scm.com/).
- During the installation:
  - Select **Git Bash** as the default terminal.
  - Enable the option to **Add Git to PATH**.

---

## 2. Install Extensions in VS Code and Sign In to GitHub
- Open VS Code and go to the **Extensions Marketplace** (`Ctrl+Shift+X`).
- Search for and install the following:
  - **Python**: For Python development.
  - **GitHub Pull Requests and Issues**: To integrate GitHub with VS Code.
- Trigger GitHub sign-in:
  - Open the Command Palette (`Ctrl+Shift+P`).
  - Type and select **GitHub Pull Requests: Sign In to GitHub**.
  - Follow the authentication steps in your browser.

---

## 3. Configure Baseline Git Commands
- Open the terminal in VS Code (`Ctrl+`).
- Set your Git global configurations:
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your-email@example.com"
  git config --global init.defaultBranch main
  git config --global core.editor "code --wait"

---

## 4. Generate SSH Key

An SSH Key allows secure, password-free authentication between your local machine and GitHub. Once added to your GitHub account, it grants access to all repositories linked to your account, enabling you to push, pull, and clone code securely.

To set it up, follow the subsequent steps: 

- In the VS Code Terminal, run:
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```
-Follow the prompts:
 - Press Enter to save the key in the default location (`~/.ssh/id_ed25519`).
 - Optionally, add a passphrase for added security.

---

## 5. Add SSH Identity in PowerShell (As Administrator)

- Open **PowerShell as Administrator**:
 - Press `Win + S`, type **PowerShell** and select **Run as Administrator**
 - Start the SSH agent: 
 ```powershell
 Start-Service ssh-agent
 ```
 - Add your SSH key to the agent:
 ```powershell
 ssh-add $HOME\.ssh\id-ed25519
 ```

---

## 6. Add SSH Key to GitHub
- Copy the public key:
```powershell
cat $HOME\.ssh\id_ed25519.pub
```
- Go to [GitHub SSH Keys Settings.](https://github.com/settings/keys).
- Klick **New SSH Key**:
 - Paste the copied key into the "Key" field.
 - Add a title (e.g. Laptop of ...).
 - Click **Add SSH Key**.

 ---

 ## 7. Test the SSH Connection
 - Verify the connection to GitHub:
 ```bash
 ssh -T git@github.com
 ```
 - Expected Output:
 ```vbnet
 Hi username! You have successfully authenticated, but GitHub does not provide shell access.
```

Like that, you established a secure connection between GitHub and your local machine or cloud-based folder.

## 8. Create a baseline folder for repository mirroring

To have a good oversight over the different repositories, it is advisable to store them within a baseline directory. This directory can either be on your local machine or in a path which automatically syncs the repos with an external cloud service, such as OneDrive. 

For instance, to create a respective OneDrive directory in your system, use the following PowerShell code:

```powershell
New-Item -ItemType Directory -Path "C:\Users\USERNAME\OneDrive\Documents\GitHub" -Force
```
When establishing new repositories, you then always first navigate to the baseline folder before cloning a repo. 

---

## 9. Create and clone a new repository 

1. **Create a New Repository on GitHub**:
 - Go to [GitHub](https://github.com/), click **+**, and select **New Repository**.
 - Fill in the repository name (e.g., `My-New-Repo`) and choose visibility (public or private).
 - Do not initialize with a README or `.gitignore`.

2. **Clone the Repository to Your Local Path**:
 - Open the terminal in VS Code.
 - Navigate to your GitHub folder:
   ```bash
   cd C:\Users\USERNAME\OneDrive\Documents\GitHub
   ```
 - Clone the repository:
   ```bash
   git clone git@github.com:your-username/My-New-Repo.git
   ```

3. **Navigate to the Repository Directory**:
 ```bash
 cd My-New-Repo
```

---

## 10. Add a File, Commit and Push Changes:

- Add files to the respective repo in VS Code
    - Python File:
    ```bash 
    code py_script.py
    ```
    - Markdown File:
    ```bash
    code markdown_file.md
    ```
- Stage the Files:
    - If you want to add multiple files:
    ```bash
    git add py_script.py markdown_file.md
    ```
    - If you want to stage all changes:
    ```bash
    git add .
    ```
- Commit the changes:
    - Commit the changes with a descriptive message.
    ```bash
    git commit -m "Add Python script and Markdown documentation."
    ```
- Push Changes to Github
    - Mirror the changes in your local repository with the GitHub repository by **pushing your changes** to the remote repository in the `main` branch:
    ```bash
    git push origin main
    ```
## 11. Branching in Git

When developing code, you usually create branches. Git branches are effectively a pointer to a snapshot of your changes. Branches allow developers to work on features, bug fixes, or experiments in isolation from the main codebase (often the main or master branch). This prevents unfinished or unstable code from affecting the main project.

### Reasons for using Git Branches 

Git Branches are essential for the following reasons: 

Branches in Git are essential for several reasons:

1. **Isolation of Work**: Branches allow developers to work on features, bug fixes, or experiments in isolation from the main codebase (often the main or master branch). This prevents unfinished or unstable code from affecting the main project.
2. **Parallel Development**: Multiple developers can work on different features or fixes simultaneously without interfering with each other's work. Each developer can create a branch for their specific task.
3. **Experimentation**: Branches provide a safe space to experiment with new ideas or technologies. If an experiment fails or is not needed, the branch can be easily deleted without impacting the main codebase.
4. **Version Control**: Branches facilitate version control by allowing different versions of the codebase to coexist. For example, you can maintain a stable version on one branch while developing new features on another.
5. **Code Review and Collaboration**: Branches make it easier to review code changes before merging them into the main branch. Pull requests can be created from branches, allowing team members to comment on and discuss changes.
6. **Simplified Merging**: When a feature or fix is complete, it can be merged back into the main branch. Git provides powerful merge tools to help resolve any conflicts that might arise during this process.

There are several branches it a Git workflow:

### Types of Git Branches

In Git, branches are categorized based on their purpose and usage in a project. Below are the main types of branches:

1. Main Branch
- **Purpose**:
  - Represents the primary, stable, production-ready state of the code.
- **Examples**:
  - `main` (default in new Git repositories).
  - `master` (default in older repositories).
- **Usage**:
  - Directly deployable code.
  - Only tested, reviewed, and approved changes are merged into this branch.

2. Feature Branches
- **Purpose**:
  - Used to develop new features or functionalities in isolation.
- **Examples**:
  - `feature-login`, `feature-user-profile`, `feature-dark-mode`.
- **Usage**:
  - Created from the main branch.
  - Allows developers to work on a specific task without impacting the main branch.
  - Merged back into the main branch after completion.

3. Bugfix Branches
- **Purpose**:
  - Used to fix bugs in the codebase.
- **Examples**:
  - `bugfix-login-error`, `bugfix-api-timeout`.
- **Usage**:
  - Created to address issues reported in the production or testing environment.
  - Often merged back into the main branch or a release branch.

 4. Release Branches
- **Purpose**:
  - Prepares the codebase for an upcoming release.
- **Examples**:
  - `release-v1.0`, `release-v2.1`.
- **Usage**:
  - Created from the main branch.
  - Focuses on finalizing the release (e.g., testing, documentation updates).
  - Merged back into `main` (for deployment) and optionally `develop` (if using a branching model like Git Flow).

5. Hotfix Branches
- **Purpose**:
  - Used for critical fixes that need to be applied to the production codebase immediately.
- **Examples**:
  - `hotfix-v1.0.1`, `hotfix-security-patch`.
- **Usage**:
  - Created directly from the main branch.
  - Merged back into `main` and other branches like `develop` to ensure the fix is reflected in all active development lines.

6. Development Branch
- **Purpose**:
  - Serves as the integration branch for ongoing development.
- **Examples**:
  - `develop`, `dev`.
- **Usage**:
  - Contains untested or experimental code.
  - Used as the base for feature branches in workflows like Git Flow.
  - Merged into `main` once the code is production-ready.

7. Experimental Branches
- **Purpose**:
  - Used for experimental or exploratory work.
- **Examples**:
  - `experiment-new-algorithm`, `test-new-framework`.
- **Usage**:
  - Created for trying out ideas or testing libraries.
  - May not be merged into the main branch and can be deleted after the experiment.

### Common Workflows Using Branches

1. **Git Flow**:
   - A structured branching model with `main`, `develop`, `feature`, `release`, and `hotfix` branches.
2. **Trunk-Based Development**:
   - Focuses on short-lived feature branches that are frequently merged into the `main` branch.
3. **GitHub Flow**:
   - Simplified model with `main` and short-lived feature branches.

By understanding and using these types of branches, you can organize your development process more effectively.

### Workflow with branches: Hands-On Example

This example demonstrates how to create a new branch, make changes, and merge it back into the `main` branch using your current repository. Let's say we have a repo called "Setup-Guide" and we want to add a Python script to it.


**Step 1: Navigate to Your Repository**

1. Open the terminal in VS Code or PowerShell.
2. Navigate to your repository folder:
   ```bash
   cd C:\Users\USERNAME\OneDrive\Documents\GitHub\Setup-Guide
   ```

**Step 2: Create a new Branch**

1. Create and switch to a new branch named `feature-hello-world`:
```bash
git checkout -b feature-hello-world
```
2. Verify that you are now on the branch:
```bash
git branch
```
The branch you're on will be highlighted with an asterisk (*)

**Step 3: Make Changes**
1. Create a new Python script
```bash
code hello_world.py
```
2. Add changes to the file
```python
print('Hello World!')
```
3. Add the file to the repo
```bash
git add hello_world.py
```
4. Commit the changes
```bash
git commit -m "Add hello_world.py script"
```

**Step 4: Push the Branch to GitHub**
1. Push the `feature-hello-world` branch to GitHub
```bash
git push origin feature-hello-world
```
2. Verify the branch is visible in your GitHub repository by visiting your repository online.Verify the branch is visible in your GitHub repository by visiting your repository online

**Step 5: Merge the Branch into `main`**

1. Switch back to the `main` branch
```bash
git checkout main
```
2. Merge the `feature-hello-world` branch:
```bash
git merge feature-hello-world
```
3. Push the updated `main` branch to GitHub:
```bash
git push origin main
```

**Step 6: Delete the Feature Branch**

1. Delete the branch locally
```bash
git branch -d feature-hello-world
```
2. Delete the branch on GitHub
```bash
git push origin --delete feature-hello-world
```




