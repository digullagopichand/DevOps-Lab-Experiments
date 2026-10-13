# Week 3 – Practice Source Code Management on GitHub

## Aim
To push and manage source code using GitHub.

## Description
This experiment demonstrates how to store source code in a GitHub repository, track changes using Git, commit files, and push the source code to a remote repository.

## Requirements
- Git
- GitHub account
- Visual Studio Code or Git Bash
- JavaScript-enabled web browser

## Files Included
- `experiment-record.pdf` – Lab experiment record
- `index.html` – Event registration form source code from Experiment 1
- `images/` – Execution screenshots
- `README.md` – Experiment documentation

## Procedure

### Step 1: Create a GitHub Repository
1. Log in to GitHub.
2. Click **New repository**.
3. Enter the repository name `Week3-SourceCode`.
4. Create the repository.

### Step 2: Clone the Repository

Replace `YOUR-USERNAME` with your GitHub username.

```bash
git clone https://github.com/YOUR-USERNAME/Week3-SourceCode.git
```

### Step 3: Enter the Repository Folder

```bash
cd Week3-SourceCode
```

### Step 4: Create the Source Code File

Create a file named `index.html` in the repository folder.

Copy the HTML and JavaScript event registration form source code from Experiment 1 into this file and save it.

### Step 5: Check Repository Status

```bash
git status
```

### Step 6: Add the Source Code

```bash
git add index.html
```

To add all files:

```bash
git add .
```

### Step 7: Commit the Changes

```bash
git commit -m "Added source code for a simple user registration form"
```

### Step 8: Push the Changes to GitHub

```bash
git push origin main
```

If the repository uses `master` as its branch, use:

```bash
git push origin master
```

### Step 9: Verify the Repository

1. Open your repository on GitHub.
2. Refresh the page.
3. Verify that `index.html` and the committed files appear.
4. Open the file to view the source code.

## All Commands in One Place

```bash
# Clone the repository
git clone https://github.com/YOUR-USERNAME/Week3-SourceCode.git

# Enter the repository
cd Week3-SourceCode

# Check status
git status

# Add source code
git add index.html

# Add all files, if required
git add .

# Commit changes
git commit -m "Added source code for a simple user registration form"

# Push changes to GitHub
git push origin main

# Check commit history
git log

# Check repository status
git status
```

## Expected Output
The source code file is uploaded to the GitHub repository. The committed changes can be viewed on GitHub.

## Result
Source code is pushed to GitHub and managed using Git version control.