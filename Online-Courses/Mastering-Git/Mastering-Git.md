---
share: true
path: Online-Courses/Mastering-Git
---
# Sources

I am using the following website to train: https://learngitbranching.js.org/?locale=en

---

# Module 1

*On the blue zone is where we begin and on the red zone is the goal to achieve. 

- Exercise 1: make two commits to complete the level

![](Learn/Notes/assets/Mastering%20Git%20-%20exercise%201%20commits.png)

```Bash
git commit 
git commit
```

- Exercise 2: Git Branches - make a new branch named `bugFix` and switch to that branch.

Branches in Git are incredibly lightweight as well. They are simply pointers to a specific commit -- nothing more. This is why many Git enthusiasts chant the mantra:

>Branch early, and branch often 

![](Learn/Notes/assets/Mastering%20Git%20-%20exercise%202%20commits.png)

```bash
git checkout -b bugFix
```

- Exercise 3: Branches and merging

Merging in Git creates a special commit that has two unique parents. A commit with two parents essentially means "I want to include all the work from this parent over here and this one over here, _and_ the set of all their parents."

Instructions:
1. Make a new branch called `bugFix`
2. Checkout the `bugFix` branch with `git checkout bugFix`
3. Commit once
4. Go back to `main` with `git checkout`
5. Commit another time
6. Merge the branch `bugFix` into `main` with `git merge`

![](Learn/Notes/assets/Mastering%20Git%20-%20exercise%203%20commits.png)

```bash
git checkout -b bugFix
git commit
git checkout main
git commit
git merge bugFix
```

- Exercise 4: Git Rebase

The second way of combining work between branches is _rebasing._ Rebasing essentially takes a set of commits, "copies" them, and plops them down somewhere else.

While this sounds confusing, the advantage of rebasing is that it can be used to make a nice linear sequence of commits. The commit log / history of the repository will be a lot cleaner if only rebasing is allowed.

> [!ai]+ AI
>
> Git rebase is a command used to move or combine a sequence of commits to a new base commit. It allows for a cleaner and more organized commit history by integrating changes from one branch onto another. By using rebase, developers can avoid creating unnecessary merge commits and maintain a linear project history.

Instructions:
1. Checkout a new branch named `bugFix`
2. Commit once
3. Go back to main and commit again
4. Check out bugFix again and rebase onto main

![](Learn/Notes/assets/Mastering%20Git%20-%20exercise%204%20commits.png)

```bash
git checkout -b bugFix
git commit
git checkout main
git commit
git checkout bugFix
git rebase main
```

---

# Module 2

- Exercise 1: HEAD

HEAD is the symbolic name for the currently checked out commit -- it's essentially what commit you're working on top of.

HEAD always points to the most recent commit which is reflected in the working tree. Most git commands which make changes to the working tree will start by changing HEAD.

Normally HEAD points to a branch name (like bugFix). When you commit, the status of bugFix is altered and this change is visible through HEAD.

Detaching HEAD just means attaching it to a commit instead of a branch. This is what it looks like beforehand.

> [!ai]+ AI
>
> The git HEAD is a pointer that represents the current position or the latest commit in the branch you are currently on.

Instructions:

let's detach HEAD from `bugFix` and attach it to the commit instead. Specify this commit by its hash. The hash for each commit is displayed on the circle that represents the commit.

![](Learn/Notes/assets/Mastering%20Git%20-%20head%20m2.png)

```bash
git checkout C4
```

- Exercise 2: Relative Refs

In the real world you'll have to use `git log` to see hashes.

For instance, the hash of the commit that introduced the previous level is `fed2da64c0efc5293610bdd892f82a58e8cbc5d8`. Doesn't exactly roll off the tongue...

The upside is that Git is smart about hashes. It only requires you to specify enough characters of the hash until it uniquely identifies the commit. So I can type `fed2` instead of the long string above.

This is why Git has relative refs. With them, you can start somewhere memorable (like the branch `bugFix` or `HEAD`) and work from there.

Relative commits are powerful, but we will introduce two simple ones here:
- Moving upwards one commit at a time with `^`
- Moving upwards a number of times with `~<num>`

Lets look at the Caret (^) operator first. Each time you append that to a ref name, you are telling Git to find the parent of the specified commit.
- So saying `main^` is equivalent to "the first parent of `main`".
- `main^^` is the grandparent (second-generation ancestor) of `main`

Instructions:
Check out the parent commit of `bugFix`. This will detach `HEAD`. You can specify the hash if you want, but try using relative refs instead!

![](Learn/Notes/assets/Mastering%20Git%20-%20exercise%202%20m2.png)

```bash
git checkout bugFix^
```

- Exercise 3: The "~" operator

Say you want to move a lot of levels up in the commit tree. It might be tedious to type `^` several times, so Git also has the tilde (~) operator.

Branch forcing: One of the most common ways I use relative refs is to move branches around. You can directly reassign a branch to a commit with the `-f` option. So something like `git branch -f main HEAD~3` moves (by force) the main branch to three parents behind HEAD.

Instructions:
Move `HEAD`, `main`, and `bugFix` to their goal destinations shown.

![](Learn/Notes/assets/Mastering%20Git%20-%20exercise%203%20m2.png)

```bash
git branch -f main C6
git checkout bugFix~3
git branch -f bugFix HEAD~1
```

