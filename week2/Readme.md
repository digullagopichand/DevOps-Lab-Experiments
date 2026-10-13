# Week 2 – Explore Git and GitHub Commands

## Aim
To explore basic Git and GitHub commands.

## Description
Git and GitHub are popular tools used for version control and collaboration in software development. This experiment covers repository initialization, file tracking, commits, branches, merging, pushing, cloning, and pull requests.

## Requirements
- Git
- GitHub account
- Visual Studio Code or Git Bash
- Internet connection for GitHub operations

## All Git and GitHub Commands

### 1. Initialize a Git Repository
```bash
git init
```

### 2. Check Repository Status
```bash
git status
```

### 3. Add Files to the Staging Area
```bash
git add <file-name>
```

To add all files:
```bash
git add .
```

### 4. Commit Changes
```bash
git commit -m "commit message"
```

### 5. View Commit History
```bash
git log
```

### 6. Undo Changes
```bash
git checkout <file-name>
```

### 7. Create a New Branch
```bash
git branch <branch-name>
```

### 8. Switch to Another Branch
```bash
git checkout <branch-name>
```

### 9. Merge Branches
```bash
git merge <branch-name>
```

### 10. Push Changes to GitHub
```bash
git push origin <branch-name>
```

### 11. Clone a Repository from GitHub
```bash
git clone <repository-url>
```

## Complete Execution Procedure

Create an empty repository named `GitExperiment` on GitHub. Replace `YOUR-USERNAME` with your GitHub username.

Run these commands one by one in the terminal:

```bash
# Create project folder
mkdir GitExperiment
cd GitExperiment

# Initialize repository
git init

# Check status
git status

# Create a sample file (Windows PowerShell)
"Hello Git and GitHub" > program.txt

# Add file
git add program.txt

# Check status
git status

# Commit changes
git commit -m "First commit"

# View commit history
git log

# Create a main branch if needed
git branch -M main

# Connect to GitHub repository
git remote add origin https://github.com/YOUR-USERNAME/GitExperiment.git

# Check remote repository
git remote -v

# Push changes to GitHub
git push -u origin main

# Create a new branch
git branch test-branch

# Switch to the new branch
git checkout test-branch

# Make and commit a change on the branch
"Testing Git branch" >> program.txt
git add program.txt
git commit -m "Updated file on test branch"

# Switch back to main
git checkout main

# Merge the branch into main
git merge test-branch

# Push merged changes
git push origin main

# View commit history
git log
```

## Clone a Repository

Run the following command from a different folder, not from inside the existing `GitExperiment` folder.

```bash
git clone https://github.com/YOUR-USERNAME/GitExperiment.git
```

## Undo Unstaged Changes

Use this command only when you want to discard unstaged changes to a file.

```bash
git checkout -- program.txt
```

## Configure Git Identity

If Git asks for your name and email, configure them once using your own details.

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

## Creating a Pull Request
1. Open your repository on GitHub.
2. Push a branch containing your changes.
3. Select the branch comparison option.
4. Click **New pull request**.
5. Review the changes and create the pull request.

## Files Included
- `experiment-record.pdf` – Lab experiment record
- `commands.txt` – Git and GitHub commands
- `images/` – Execution screenshots
- `README.md` – Experiment documentation

## Expected Output
The commands demonstrate repository initialization, staging, committing, branch creation, switching, merging, cloning, and pushing changes to GitHub.

## Result
Basic Git and GitHub commands for source code version control and collaboration are explored.