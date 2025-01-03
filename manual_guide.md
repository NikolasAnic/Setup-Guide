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
- In the VS Code Terminal, run:
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```
-Follow the prompts:
 - Press Enter to save the key in the default location (`~/.ssh/id_ed25519`).
 - Optionally, add a passphrase for added security.

