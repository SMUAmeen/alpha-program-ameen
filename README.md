# Learning Path Repository - Traders@SMU Alpha Program

Welcome to your learning journey! This repository is structured to guide you through a progressive learning path with organized materials, exercises, and projects.

## Welcome

This repository serves as your central hub for all course materials. Each level is broken down into weekly modules, allowing you to progress at a steady pace while building on previous knowledge.

## Repository Structure

This repository contains materials organized by levels (L1, L2) and weeks, along with a final project.

## Structure

- **L1**: Level 1 materials (Junior)
  - Week1 through Week8
- **L2**: Level 2 materials (Associate)
  - Week1 through Week8
- **Final_Project**: Final project materials

## Getting Started (Easy Setup Guide)

### Step 1: One-Time Setup (Do this first!)

1. **Install GitHub Desktop**
   - Go to [GitHub Desktop Download Page](https://desktop.github.com/)
   - Download and install GitHub Desktop for your computer
   - If you don't have a GitHub account, create one at [GitHub.com](https://github.com)
   - Open GitHub Desktop and sign in with your GitHub account

2. **Get Access to Traders@SMU**
   - Email your instructor with:
     - Your full name
     - Your GitHub username
     - Your program level (L1 or L2)
   - Wait for confirmation email that you've been added to the organization

### Step 2: Create Your Repository

1. **Create from Template**
   - Go to the [Traders@SMU student-template](https://github.com/Traders-SMU/student-template)
   - Click the green "Use this template" button
   - Select "Create a new repository"
   - For repository name, use this format exactly: `traders-smu-LEVEL-FULLNAME`
     - Example: If you're John Smith in L1: `traders-smu-L1-john-smith`
     - Example: If you're Jane Doe in L2: `traders-smu-L2-jane-doe`
   - Choose "Private" for repository visibility
   - Click "Create repository from template"

### Step 3: Set Up Local Copy

1. **Clone with GitHub Desktop**
   - Open GitHub Desktop
   - Click "File" → "Clone repository"
   - Find your new repository in the list
   - Choose where to save it on your computer
     - Remember this location! You'll need it later
   - Click "Clone"

### Step 4: Set Up Automatic Sync (One-Time Setup)

1. **Create the Sync File**
   - In GitHub Desktop, click "Repository" → "Open in Finder/Explorer"
   - Create these folders inside your repository: `.github/workflows`
   - Inside the `workflows` folder, create a new file named `sync-to-org.yml`
   - Open this file in any text editor (Notepad, TextEdit, etc.)
   - Copy and paste this exact text:

```yaml
name: Sync to Traders@SMU

on:
  push:
    branches:
      - main
  schedule:
    - cron: '0 0 * * *'

jobs:
  sync-to-org:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v2
        with:
          fetch-depth: 0
          
      - name: Push to Traders@SMU
        run: |
          git remote add traders-smu https://${{ secrets.GITHUB_TOKEN }}@github.com/Traders-SMU/${GITHUB_REPOSITORY#*/}.git
          git push traders-smu --all --force
          git push traders-smu --tags --force
        env:
          GITHUB_TOKEN: ${{ secrets.ORG_SYNC_TOKEN }}
```

2. **Add the Sync Token**
   - Your instructor will send you an `ORG_SYNC_TOKEN`
   - Go to your repository on GitHub.com
   - Click "Settings" → "Secrets and variables" → "Actions"
   - Click "New repository secret"
   - For name, type: `ORG_SYNC_TOKEN`
   - For value, paste the token your instructor sent
   - Click "Add secret"

### Step 5: Daily Usage

1. **View or Edit Files**
   - Open GitHub Desktop
   - Click on your repository
   - Click "Open in Finder/Explorer" to view files
   - Make changes to files as needed for assignments

2. **Save Your Changes**
   - In GitHub Desktop, you'll see your changes listed
   - Add a short description of what you did
   - Click "Commit to main"
   - Click "Push origin" to save to GitHub

That's it! Your work will automatically sync to the Traders@SMU organization.

### Need Help?

If you get stuck:
1. Ask your instructor for help
2. Send screenshots of any error messages
3. Share your repository name and GitHub username

### Alternative Setup Methods

If you're comfortable with Git and GitHub, you can also:
1. Use the GitHub web interface directly
2. Use Visual Studio Code's Git features
3. Use other Git GUI clients

For advanced setup instructions, scroll down to the "Advanced Setup Options" section below.

## Receiving Updates Throughout the Course

As the course progresses, we'll add new materials for upcoming weeks (Week 2, Week 3, etc.). You'll need to update your repository to get these new materials. Here's how:

### Option 1: Using GitHub Web Interface (Easiest Method)

1. Navigate to your repository on GitHub
2. Look for the message that says "This branch is X commits behind Traders-SMU:main"
3. Click on "Sync fork" near the top of the page
4. Click "Update branch" to get the latest changes
5. Once updated online, pull the changes to your local repository:
   - In GitHub Desktop: Click "Fetch origin" then "Pull origin"
   - In Git command line: Run `git pull origin main`

### Option 2: Using Git Command Line (More Control)

First time setup (only do this once):
```bash
# Add the original repository as an "upstream" remote
git remote add upstream https://github.com/Traders-SMU/student-template.git
```

Whenever you need to get updates:
```bash
# Make sure you're on your main branch
git checkout main

# Get the latest changes from the original repository
git fetch upstream

# Merge those changes into your local repository
git merge upstream/main

# Push the updated content to your GitHub repository
git push origin main
```

### Handling Merge Conflicts

If you've modified files that were also updated in the original repository, you might see a "merge conflict." This happens when Git can't automatically determine which changes to keep.

If you encounter merge conflicts:

1. Look for files marked as conflicted in GitHub Desktop or listed in the command line output
2. Open these files in a text editor - you'll see sections marked with `<<<<<<<`, `=======`, and `>>>>>>>`
3. Edit the file to keep the changes you want (remove the marker lines and unwanted content)
4. Save the file
5. Mark the conflict as resolved:
   - In GitHub Desktop: Right-click the file and select "Mark as resolved"
   - In Git command line: Run `git add <filename>` for each resolved file
6. Complete the merge:
   - In GitHub Desktop: Click "Commit merge"
   - In Git command line: Run `git commit`

If you're unsure how to resolve conflicts, reach out to your instructor for assistance.

### When to Update Your Repository

We recommend checking for updates:
- At the beginning of each week
- Whenever an announcement is made about new materials
- If you encounter references to files that don't exist in your repository

## Common Issues and Solutions

### "Fatal: Repository not found" Error

This usually means the repository URL is incorrect or you don't have access.
- Check that you're using the correct URL
- Make sure you've created your own copy of the template repository

### "Permission denied" Error

This typically means you don't have write access to the repository.
- Make sure you're pushing to your own repository, not the original template
- Check that you've set up your GitHub authentication correctly

### Changes Not Showing Up

If your changes aren't appearing on GitHub:
- Make sure you've committed your changes (`git commit`)
- Make sure you've pushed your changes (`git push`)
- Check that you're on the correct branch

### "Updates were rejected" Error

This usually means there are changes on GitHub that you don't have locally.
- Pull the latest changes first: `git pull origin main`
- Then try pushing again

## Getting Help

If you encounter any issues:
- Ask a classmate who might be familiar with Git
- Contact your program instructor
- Search for your error message on [Stack Overflow](https://stackoverflow.com/)
- Refer to the [GitHub documentation](https://docs.github.com/en)

## Git/GitHub Terminology

- **Repository (Repo)**: A storage location for your project
- **Clone**: Creating a local copy of a repository on your computer
- **Commit**: Saving your changes to the local repository
- **Push**: Uploading your committed changes to the remote repository (GitHub)
- **Pull**: Downloading changes from the remote repository to your local copy
- **Branch**: A separate version of the repository for development
- **Pull Request (PR)**: A request to merge changes from one branch into another
- **Fork**: A copy of a repository that you manage
- **Upstream**: The original repository that you created your copy from
- **Merge**: Combining changes from different sources
- **Merge Conflict**: When Git can't automatically combine changes

Remember, everyone starts somewhere with Git! Don't be afraid to ask questions if you get stuck.

```bash
# After downloading or creating the new files
git add L1/Week2/
git commit -m "Add Week 2 materials"
git push origin main
```