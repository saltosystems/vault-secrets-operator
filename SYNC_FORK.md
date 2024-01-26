To update your forked repository with the latest changes from the original repository (upstream), you can follow these steps using the command line. Make sure you have Git installed on your machine. Here's a step-by-step guide:

### Step 1: Set Up Upstream Remote (if not done previously)
If you haven't set up the upstream remote, add it:

```bash
# Add the original repository as the upstream remote
git remote add upstream https://github.com/hashicorp/vault-secrets-operator.git
```

### Step 2: Create a Backup Branch

```bash
# Assuming you are currently on your main branch
git branch release_<current_version>

# This will create a new branch named 'release_<current_version>' pointing to the same version tag as your current branch
```

### Step 3: Fetch the Latest tags from Upstream

```bash
# Fetch the latest tags from upstream
git fetch upstream --tags
```

### Step 4: Create branch from tag

```bash
# Assuming you are currently on your main branch
git branch upstream/<new_version> <new_version>
```

### Step 5: Rebase

Perform the rebase:

```bash
# Rebase your main branch onto the new version tag
git rebase upstream/<new_version>

# Resolve conflicts (if any) and continue the rebase
```


### Step 6: Update the version tag

```bash
# Update the version tag to point to the latest commit
git tag -f <new_version>
```

### Step 7: Force push

```bash
# Force push to your forked repository
git push origin main --force
```

### Step 8: In Case of Issues, Restore from Backup

If something goes wrong or you need to revert the changes, you can easily switch back to the backup branch:

```bash
# Switch to the backup branch
git checkout release_<current_version>

# Force push the backup branch to restore it
git push origin release_<current_version> --force
```

This way, you always have a backup branch pointing to the state before the rebase and force push. If anything unexpected happens, you can quickly switch back to the backup branch.

Please note that force-pushing and rewriting history can have implications, especially in a collaborative environment. It's crucial to communicate such actions with your team and follow any established best practices or guidelines. 
