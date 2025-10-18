# Git Flow Manual Setup for Azure DevOps

Since you're using Azure DevOps, here's the manual setup I recommend:

## Step 1. Set up your branches manually
```
cd ~/Workspace/your-repo-name
git status
git branch -a
# Make sure you're starting from main
git checkout main

# Create and push develop branch
git checkout -b develop
# Push develop to Azure DevOps
git push -u origin develop

# Go back to main
git checkout main

# Verify both branches exist remotely
git branch -a
```

You should see:
```
* main
  develop
  remotes/origin/main
  remotes/origin/develop
```

## Step 2. Configure branch policies in Azure DevOps
Go to your Azure DevOps project → Repos → Branches:
For main branch:
- Enable "Require a minimum number of reviewers" (1+)
- Enable "Check for linked work items"
- Enable "Limit merge types" (squash merge recommended)
For develop branch (optional but recommended):
- Enable "Require a minimum number of reviewers"
- Consider enabling "Build validation"

## Step 3: Proper Workflow with Protected Branches
Now your workflow becomes:

For features to develop:
```
# Create feature branch
git checkout develop
git checkout -b feature/my-feature

# Make changes and push
git add .
git commit -m "My feature work"
git push origin feature/my-feature

# Then go to Azure DevOps and create Pull Request:
# - Source: feature/my-feature
# - Target: develop
# - Add reviewers
# - Link work item
```