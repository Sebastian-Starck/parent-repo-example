# Useful Commands

Common used commands for managing the tag & frontend submodule.

### Check Current State

```bash
# See all tags
git tag -l

# See current submodule commit
git submodule status

# See what frontend commit a specific backend tag uses
git show <tag>:frontend
```

### Checkout submodule branch
```bash
# Update submodule
git submodule update --remote frontend
# Checkout a specific branch in the frontend submodule
git submodule set-branch -b <branch-name> frontend
```

### Emergency Rollback

```bash
# Rollback to previous version
git checkout v1.0  # This gets exact state including frontend

# Create emergency branch if needed
git checkout -b emergency-rollback v1.0
```


### Branch Cleanup

```bash
# After rebasing, clean up hotfix branches
git branch -d hotfix/branch-name

# Force delete if needed
git branch -D hotfix/branch-name
```