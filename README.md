# Git Playground
## Resource
### How git rebase works  
[![How git rebase works](https://img.youtube.com/vi/f1wnYdLEpgI/0.jpg)](https://www.youtube.com/watch?v=f1wnYdLEpgI)

### Difference between git merge, git cherry pick and git rebase  
[![Difference between git merge, cherry-pick, and rebase](https://img.youtube.com/vi/i657Bg_HAWI/0.jpg)](https://www.youtube.com/watch?v=i657Bg_HAWI&t=30s)

![Difference](/imgs/01.png)

## Git Graph
### git rebase
**Before**
![Before](/imgs/02.png)

<pre>
git rebase main
</pre>

**After**
![After](/imgs/03.png)

### git merge
**Before**
![Before](/imgs/04.png)

<pre>
git checkout main
git merge my-cool-feature
</pre>

**After**
![After](/imgs/05.png)

### git cherry pick [commit hash code]
**Before**<br>
![Before](/imgs/06.png)

<pre>
git checkout main
git cherry-pick 0e9beab4
</pre>

**After**<br>
![After](/imgs/07.png)

### ✅ Key Point: `git cherry-pick` does **not** create a merge relationship

**What `cherry-pick` does:**
- Copies a specific commit from another branch to the current branch.
- Does **not** create a merge commit.
- Does **not** show a branch connection in the Git graph (no "merge arrow").

**So in Git Graph, it looks like:**
- The two branches evolve independently.
- The cherry-picked commit appears as a **new commit** in your current branch,  
  but there is **no visual connection** to the original branch.


## 🙅 Easy mistake!!!
### git merge main vs git merge my-cool-feature
The difference lies in which branch you're currently on and which branch you're merging into it.

🧭 General Rule:
git merge <branch-name>
means: "Merge the changes from <branch-name> into my current branch."

✅ git merge main
You are on another branch, e.g. my-cool-feature, and you want to bring in the latest changes from main.
<pre>
git checkout my-cool-feature
git merge main
</pre>
🟢 Use case: You want to update your feature branch with the latest commits from main before continuing work.

✅ git merge my-cool-feature
You are on the main branch, and you want to bring in the changes from my-cool-feature.
<pre>
git checkout main
git merge my-cool-feature
</pre>
🟢 Use case: Your feature is complete and ready to be merged into main.

## ✅ Push to GitHub

If your local branch is `main`:

<pre>
git push -u origin main
</pre>

If you're on a different branch (e.g., master or any other):
<pre>
git push -u origin your-branch-name
</pre>

## ✅ Pull from GitHub

To fetch the latest changes from the remote repository and merge them into your current branch:

<pre>
git pull origin main
</pre>

Replace main with your branch name if you're working on a different branch:
<pre>
git pull origin your-branch-name
</pre>

# ✅ What is `git pull --rebase`?

## By default, `git pull` performs:

<pre>
git fetch origin
git merge origin/main
</pre>
This can create a merge commit, leading to a messy commit history with unnecessary branches.
### Graph
🧪 git pull (merge):<br>
A---B---C (origin/main)

D---E (local)

After pull:<br>
A---B---C-------F (merge commit)<br>
\ /<br>
D---E

## 🔄 git pull --rebase does:
<pre>
git fetch origin
git rebase origin/main
</pre>
It re-applies your local commits on top of the latest remote commits, keeping the history linear and clean.

### Graph
#### 🔁 git pull --rebase:
A---B---C (origin/main)

D'---E' (rebased)
Your local commits are replayed on top of the latest remote history.