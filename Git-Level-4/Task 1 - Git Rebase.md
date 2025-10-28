# Task 1: Git Rebase

## Question

The Nautilus application development team has been working on a project repository `/opt/blog.git`. This repo is cloned at `/usr/src/kodekloudrepos` on `storage server` in `Stratos DC`. They recently shared the following requirements with DevOps team:

**Task:**

One of the developers is working on `feature` branch and their work is still in progress, however there are some changes which have been pushed into the `master` branch, the developer now wants to `rebase` the `feature` branch with the `master` branch without loosing any data from the `feature` branch, also they don't want to add any `merge commit` by simply merging the `master` branch into the `feature` branch. Accomplish this task as per requirements mentioned.

Also remember to push your changes once done.

---

# Solution

## 🧭 Task Summary
Rebase the `feature` branch with the latest changes from `master` **without merge commits**, keeping all feature commits intact and pushing the result to the remote repository.

---

## ✅ Step-by-Step Solution

### 1. Go to the repo directory
```bash
cd /usr/src/kodekloudrepos/blog
```

> Make sure you are inside the cloned repository (not the bare one at `/opt/blog.git`).

---

### 2. Check the existing branches
```bash
git branch
```

If you are not on the `feature` branch, switch to it:
```bash
git checkout feature
```

---

### 3. Make sure both branches are up to date
Fetch the latest changes from the remote repository:
```bash
git fetch origin
```

Update your local `master` branch:
```bash
git checkout master
git pull origin master
```

Switch back to `feature`:
```bash
git checkout feature
```

---

### 4. Start the rebase
```bash
git rebase master
```

This replays your `feature` branch commits on top of the updated `master` branch (no merge commits created).

---

### 5. Resolve any conflicts (if any)
If you encounter conflicts:
```bash
git status
```
Edit the conflicting files, then:
```bash
git add <file>
git rebase --continue
```
Repeat until the rebase is completed.

If needed, abort the rebase:
```bash
git rebase --abort
```

---

### 6. Push the rebased branch to the remote
Since rebase rewrites history, use a **force push**:
```bash
git push origin feature --force
```

> ⚠️ Use `--force` carefully to avoid overwriting other developers' work.

---

## 🧩 Verification
To verify the rebase was successful:
```bash
git log --oneline --graph --decorate --all
```

You should see the `feature` commits after the latest `master` commits, forming a clean, linear history.

---

## 🏁 Summary of Commands
```bash
cd /usr/src/kodekloudrepos/blog
git fetch origin
git checkout master
git pull origin master
git checkout feature
git rebase master
# (resolve conflicts if any)
git push origin feature --force
```

---

## 💡 Notes
- **Rebase** moves your branch commits on top of another branch, creating a linear history.
- **Merge** adds an extra merge commit that may clutter history.
- Rebasing is cleaner for feature branches before merging into `master`.