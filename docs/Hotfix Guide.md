
# Hotfix Guide

A simple guide for hotfixing

> ## Important:
> 
> - **Always branch from tags for hotfixes, not from main branch**
> - **Deploy hotfix tags first, then rebase to main later**


## Frontend hotfixes

Hotfixing frontend requires the creation of a new branch,
forked out of the commit referenced in the latest tag.

![frontend-hotfix.png](images/frontend-hotfix.png)

### Lookup the commit tracked in the submodule for the latest tag

```bash
git show v1.0.0:frontend 
```

### Create frontend hotfix branch

In the frontend repo, create a new branch from this commit

```bash
git checkout -b hotfix/fix-user-login $FRONTEND_COMMIT
```

### Commit fixes to frontend repo
```bash
git add .
git commit -m "hotfix: fix null pointer in login component"
```

### Update backend with frontend changes

```bash
cd frontend/
# Point to your hotfix branch
git checkout hotfix/fix-user-login
cd ../
# Update the build
./build.sh
```

### Commit fixes to backend repo

```bash
# Create a new hotfix branch in the backend repo
git checkout -b hotfix/fix-user-login v1.0.0
# Add the updated frontend files
git add frontend/ public/
# Commit the changes
git commit -m "Hotfix v1.1: Frontend login component fix"
```

### Tag hotfix

```bash
git tag -a v1.1 -m "Hotfix v1.1: Frontend login component fix"
```

### Ready to deploy

Now we can checkout the tag in the server

### Cleanup

With the fix deployed, now we can move our fixes back to the main branches

```bash
cd frontend/
git checkout main
git rebase hotfix/fix-user-login
git branch -d hotfix/fix-user-login
git push origin main --tags
```

```bash
cd ../
git checkout main
git rebase HEAD~1  # Rebase the hotfix commit
git push origin main --tags
```

## Backend Hotfixes

Backend hotfixes are straightforward. 
You can create a new tag based on the current version of the backend.

![img.png](img.png)

### Create backend hotfix branch

```
git checkout -b hotfix/fix-user-login v1.0.0
```

### Commit fixes to backend repo

```bash
git add .
git commit -m "hotfix: fix null pointer in login component"
```

### Tag hotfix

```bash
git tag -a v1.1 -m "Hotfix v1.1: Backend login component fix"
```

### Push hotfix tag

```bash
git push origin main --tags
```

### Ready to deploy

Now we can check out the tag in the server

### Cleanup
With the fix deployed, now we can move our fixes back to the main branches

```bash
git checkout main
git rebase hotfix/fix-user-login
git branch -d hotfix/fix-user-login
git push origin main --tags
```

### Backend & Frontend hotfix

If you need to fix both backend and frontend, you can follow the steps for both frontend and backend hotfixes.


