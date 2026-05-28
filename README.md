# PP5

## Goal

In this exercise you will:

* Use Git **locally** on your own machine: create branches, make commits, and merge them back.
* Set up and interact with a **bare** Git repository on an SSH‐accessible server (e.g. **vorlesungsserver**, or any machine you have SSH access to).
* Push and pull to/from **GitHub** and the **THGA GitLab** server.
* Practice **forking** an existing repo, making changes, and submitting a **Pull Request** (on GitHub) or **Merge Request** (on GitLab).

**Important:** Start a stopwatch when you begin and work uninterruptedly for **90 minutes**. Once time is up, stop immediately and document exactly where you had to pause.

---

## Workflow

1. **Fork** this repository
2. **Modify & commit** your solution
3. **Submit your link for Review**

---

## Prerequisites

* Several starter repos are available here:
  [https://github.com/orgs/STEMgraph/repositories?q=Git%3A](https://github.com/orgs/STEMgraph/repositories?q=Git%3A)
* Ensure you have **SSH access** to a remote server (e.g., “vorlesungsserver”).
* Throughout, consult Git’s built-in man-pages (`git help <command>`) for explanations and options.

---

## Tasks

### Task 1: Local Git – Branching & Merging

1. Create a new directory in your home directory and initialize a repository in it. 
2. In one of your cloned repos, initialize a new branch called `feature-1`.
3. On `feature-1`, create a file `feature.txt` containing a short description of what you’re doing.
4. Commit your changes, then switch back to `master` (or `main`), and merge `feature-1` into your `master`.
5. Resolve any merge conflicts (if they arise) by hand, then commit the merge. 

**Your Commands & Output**

```bash
# Paste here the sequence of git commands you ran
# and the relevant terminal output (e.g., branch listing, merge messages)
mkdir git-PP5
cd git-PP5
git init
   Initialized empty Git repository in C:/Users/Konstamonster/Desktop/git-PP5/.git/
touch readme.md
git add readme.md
git commit -m "Initial commit"
   [master (root-commit) 2606f19] Initial commit
   1 file changed, 0 insertions(+), 0 deletions(-)
   create mode 100644 readme.md
git checkout -b feature-1
   Switched to a new branch 'feature-1'
echo "I am currently learning how to use Git branches and merge them." > feature.txt
git add feature.txt
git checkout master
git merge feature-1
   Updating 2606f19..794a5fb
   Fast-forward
   feature.txt | 1 +
   1 file changed, 1 insertion(+)
   create mode 100644 feature.txt
git log master
   commit 794a5fb6de28edf587e4c639908a5da03fb685a8 (HEAD -> master, feature-1)
   Author: unknown <KonstantinMoser@stud.thga.de>
   Date:   Tue May 26 16:08:10 2026 +0200

       Add feature.txt with description

   commit 2606f194b73a5e0e9439548b37804a66966b0dd8
   Author: unknown <KonstantinMoser@stud.thga.de>
   Date:   Tue May 26 16:04:33 2026 +0200

       Initial commit


****
```

---

### Task 2: Bare Repository on an SSH Server

1. On your SSH server (e.g., “vorlesungsserver”), create a **bare** repo at `~/repos/myproject.git`:

   ```bash
   ssh youruser@vorlesungsserver \
     "mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare"
   ```
2. On your local machine, add it as a remote named `origin-ssh`:

   ```bash
   git remote add origin-ssh youruser@vorlesungsserver:~/repos/myproject.git
   ```
3. Push your `master` branch to `origin-ssh`, then clone it into a fresh directory to verify.

**Your Commands & Output**

```bash
# Paste here the push & clone commands and outputs
(After running the given commands)
git push -u origin-ssh master
mkdir fresh_dir
cd fresh_dir
git clone Vorlesung:~/repos/myproject.git myproject-verify
   Cloning into 'myproject-verify'...
   remote: Enumerating objects: 3, done.
   remote: Counting objects: 100% (3/3), done.
   remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
   Receiving objects: 100% (3/3), done.

```

---

### Task 3: GitHub & THGA GitLab

1. On [GitHub](github.com), create a new empty repo under your account named `myproject-gh`.
2. On [THGA GitLab](gitlab.thga.de), create a new project named `myproject-gl`.
3. In your local repository, add these as remotes:

   ```bash
   git remote add github  git@github.com:YOUR_USERNAME/myproject-gh.git
   git remote add gitlab  git@gitlab.thga.de:YOUR_USERNAME/myproject-gl.git
   ```
4. Push your `master` branch to both `github` and `gitlab` remotes.

> Hint: You are just adding two more bare-remotes to your already existing repository!

**Your Commands & Output**

```bash
# Paste here the remote‐adding & push outputs
git remote add github git@github.com:KonstantinM08/myproject-gh.git
git remote add gitlab git@gitlab.thga.de:Konstantin.Moser/myproject-gl.git
git remote -v
    github  git@github.com:KonstantinM08/myproject-gh.git (fetch)
    github  git@github.com:KonstantinM08/myproject-gh.git (push)
    gitlab  git@gitlab.thga.de:Konstantin.Moser/myproject-gl.git (fetch)
    gitlab  git@gitlab.thga.de:Konstantin.Moser/myproject-gl.git (push)
    origin  https://github.com/KonstantinM08/myproject-gh.git (fetch)
    origin  https://github.com/KonstantinM08/myproject-gh.git (push)
    origin-ssh      KonstantinMoser@128.140.85.215:~/repos/myproject.git (fetch)
    origin-ssh      KonstantinMoser@128.140.85.215:~/repos/myproject.git (push)
#Before doing pushing main to github and GitLab I had to define an ssh-key as learned from the previous exercises. Becouse of reasons
#of convenience and readability I only show the commands for github, the process of defiening a key for gitlab is similar.
$ ssh-keygen -t rsa -b 4096 -C "konstantin.m@mail.de"
   Generating public/private rsa key pair.
   Enter file in which to save the key (/c/Users/Konstamonster/.ssh/id_rsa):
   Enter passphrase for "/c/Users/Konstamonster/.ssh/id_rsa" (empty for no passphrase):
   Enter same passphrase again:
   Your identification has been saved in /c/Users/Konstamonster/.ssh/id_rsa
   Your public key has been saved in /c/Users/Konstamonster/.ssh/id_rsa.pub
   The key fingerprint is:
   SHA256:oIis7sG/uEQoX8dPZBtrEC4hN9osDRm2N7Il3b3pWbE konstantin.m@mail.de
   The key's randomart image is:
   +---[RSA 4096]----+
   |  =o+ .          |
   | ..@ = o         |
   |  * X = = .      |
   |o. O = = * o     |
   |+oo o o S E      |
   |=. . . = o       |
   |.+.     +        |
   |o +              |
   |.=.o.            |
   +----[SHA256]-----+
cat ~/.ssh/id_rsa.pub # the output of this command can be used to establish a new ssh-key on github using the interface when #accessing github via webpage

git push -u github main
   Enumerating objects: 3, done.
   Counting objects: 100% (3/3), done.
   Writing objects: 100% (3/3), 220 bytes | 220.00 KiB/s, done.
   Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
   To github.com:KonstantinM08/myproject-gh.git
    * [new branch]      main -> main
   branch 'main' set up to track 'github/main'.
   
git push -u gitlab main
   Enumerating objects: 3, done.
   Counting objects: 100% (3/3), done.
   Writing objects: 100% (3/3), 220 bytes | 220.00 KiB/s, done.
   Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
   To gitlab.thga.de:Konstantin.Moser/myproject-gl.git
   * [new branch]      main -> main
   branch 'main' set up to track 'gitlab/main'
```

---

### Task 4: Fork, Modify, and Pull/Merge Request

1. On GitHub, **fork** one of the repos from the STEMgraph org.
2. Clone your fork locally, create a branch `pp5-changes`, and make a small change (e.g., update the README).
3. Commit and push `pp5-changes` to **your** fork, then open a **Pull Request** against the original repo.
4. Repeat on THGA GitLab: fork another students repository, clone, branch, change, push, and open a **Merge Request**. If your peers opened a merge request to your repository, review and merge or decline it!

**Your PR/MR Links & Descriptions**

* GitHub PR: *paste URL and a one-sentence summary*
* GitLab MR: *paste URL and a one-sentence summary*

---

**Remember:** Stop working after **90 minutes** and record where you stopped!
