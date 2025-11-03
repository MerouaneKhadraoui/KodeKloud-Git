# Task 2: Manage Git Repositories

## Question

A new developer just joined the Nautilus development team and has been assigned a new project for which he needs to create a new repository under his account on Gitea server. Additionally, there is some existing data that need to be added to the repo. Below you can find more details about the task:

**Task:**

Click on the `Gitea UI` button on the top bar. You should be able to access the `Gitea` UI. Login to `Gitea` server using username `max` and password `Max_pass123`.

1. Create a new git repository `story_ecommerce` under max user.

2. SSH into `storage server` using user `max` and password `Max_pass123` and clone this newly created repository under user `max` home directory i.e `/home/max`.

3. Copy all files from location `/usr/sysops` to the repository and commit/push your changes to the `master` branch. The commit message must be `"add stories"` (must be done in single commit).

4. Create a new branch `max_apps` from master.

5. Copy a file `story-index-max.txt` from location `/tmp/stories/` to the repository. This file has a typo, which you can fix by changing the word `Mooose` to `Mouse`. Commit and push the changes to the newly created branch. Commit message must be `"typo fixed for Mooose"` (must be done in single commit).

`Note:` For these kind of scenarios requiring changes to be done in a web UI, please take screenshots so that you can share it with us for review in case your task is marked incomplete. You may also consider using a screen recording software such as loom.com to record and share your work.

---

# Solution

## 1️⃣ Login to Gitea UI

1. Click the **“Gitea UI”** button on the top bar in the lab.
2. Login with the following credentials:
   ```bash
   username: max
   password: Max_pass123
   ```
3. Click on **“+” → New Repository**.
4. Fill in the details:
   - **Repository Name:** `story_ecommerce`
   - **Visibility:** Public (or default)
   - **Description:** optional
5. Click **Create Repository**.

---

## 2️⃣ Clone Repository on Storage Server

SSH into the **storage server**:

```bash
ssh max@storage
# password: Max_pass123
```

Change to the home directory and clone the repo:

```bash
cd /home/max
git clone http://<GITEA_URL>/max/story_ecommerce.git
cd story_ecommerce
```

> Replace `<GITEA_URL>` with your actual Gitea host (e.g., `gitea.stratos.xfusioncorp.com:3000`).

---

## 3️⃣ Copy Files and Push to master

Copy all files from `/usr/sysops` into the repository:

```bash
cp -r /usr/sysops/* .
```

Add, commit, and push to the master branch:

```bash
git add .
git commit -m "add stories"
git push origin master
```

---

## 4️⃣ Create a New Branch

Create and switch to a new branch named `max_apps`:

```bash
git checkout -b max_apps
```

---

## 5️⃣ Fix Typo in story-index-max.txt

Copy the file from `/tmp/stories/` into the repository:

```bash
cp /tmp/stories/story-index-max.txt .
```

Fix the typo (`Mooose` → `Mouse`) using `sed`:

```bash
sed -i 's/Mooose/Mouse/g' story-index-max.txt
```

Commit and push the fix to the new branch:

```bash
git add story-index-max.txt
git commit -m "typo fixed for Mooose"
git push origin max_apps
```

---

## ✅ Verification Checklist

- [x] Repository `story_ecommerce` exists under **user max**
- [x] Files from `/usr/sysops` added on **master** branch with commit message `"add stories"`
- [x] Branch `max_apps` created successfully
- [x] File `story-index-max.txt` fixed and pushed with commit message `"typo fixed for Mooose"`

---

**Author:** *Merouane KHADRAOUI*  
**Date:** 2025‑11‑03