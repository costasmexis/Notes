# Git
- Git is a source control software, similar to many others out there.
- It follows all the same rules and concepts that any source control follows
- The most popular source control software in the world

## Git VS GitHub
### GitHub
- GitHub is an application allowing you to store remote repositories
- You can interact with you GitHub repository through the `push/pull` system on your local machine
- GitHub is used primarily to allow other people to add to the project
- GitHub allows more people that just yourself to see and interact with the repository

### Differences
- Git is a source control software allowing you to take snapshots and distribute your creations & modifications over time
- GitHub is an application allowing you to store and interact with your repository on a remote server, as adding more features
- Git is the bones and flesh of source control, while GitHub gives you the platform to work with you repository easier

# Git Basics
## The Git workflow
- Repositories, usually called 'repos', store the full history and source control of a project
- Most repositories are stored on GitHub, while core contributors make copies of the repo on their machine and update the repo using the push/pull system
- Any repository stored somewhere other than locally is called a 'remote repository'

## Some basics
Use `git status` to check the _Staging Area_.
Use `git rm --cached <file>` to remove file from _Staging Area_.

## Undoing changes
With the `--amend` flag, you can alter the _most-recent_ commit.
`$ git commit --amend`
If your Working Directory is clean (meaning there aren't any uncommitted changes in the repository), then running `git commit --amend` will let you provide a new commit message. Your code editor will open up and display the original commit message. Just fix a misspelling or completely reword it! Then save it and close the editor to lock in the new commit message.

Alternatively, `git commit --amend` will let you include files (or changes to files) you might've forgotten to include. Let's say you've updated the color of all navigation links across your entire website. You committed that change and thought you were done. But then you discovered that a special nav link buried deep on a page doesn't have the new color. You _could_ just make a new commit that updates the color for that one link, but that would have two back-to-back commits that do practically the exact same thing (change link colors).

Instead, you can amend the last commit (the one that updated the color of all of the other links) to include this forgotten one. To do get the forgotten link included, just:
-   edit the file(s)
-   save the file(s)
-   stage the file(s)
-   and run `git commit --amend`

So you'd make changes to the necessary CSS and/or HTML files to get the forgotten link styled correctly, then you'd save all of the files that were modified, then you'd use `git add` to stage all of the modified files (just as if you were going to make a new commit!), but then you'd run `git commit --amend` to update the most-recent commit instead of creating a new one.

Using `$ git diff` Git show you the changes you' ve saved, but not yet committed.

### Git Revert & Reset
When you tell Git to **revert** a specific commit, Git takes the changes that were made in commit and does the exact opposite of them Git **revert** is a little bit safer. It goes back in time to only one commit. It looks at this commit and reverse the changes and then creates a new commit saying that it reverted the changes. 
Usage: `git revert [commit SHA]`

At first glance, _resetting_ might seem coincidentally close to _reverting_, but they are actually quite different. Reverting creates a new commit that reverts or undos a previous commit. Resetting, on the other hand, _erases_ commits!  Git **Reset** is the more dangerous option.

#### Ancestry References
You already know that you can reference commits by their SHA, by tags, branches, and the special `HEAD` pointer. Sometimes that's not enough, though. There will be times when you'll want to reference a commit relative to another commit. For example, there will be times where you'll want to tell Git about the commit that's one before the current commit...or two before the current commit. There are special characters called "Ancestry References" that we can use to tell Git about these relative references. Those characters are:

-   `^` – indicates the parent commit
-   `~` – indicates the _first_ parent commit

Here's how we can refer to previous commits:

-   the parent commit – the following indicate the parent commit of the current commit
    -   HEAD^
    -   HEAD~
    -   HEAD~1
-   the grandparent commit – the following indicate the grandparent commit of the current commit
    -   HEAD^^
    -   HEAD~2
-   the great-grandparent commit – the following indicate the great-grandparent commit of the current commit
    -   HEAD^^^
    -   HEAD~3

The main difference between the `^` and the `~` is when a commit is created _from a merge_. A merge commit has _two_ parents. With a merge commit, the `^` reference is used to indicate the _first_ parent of the commit while `^2` indicates the _second_ parent. The first parent is the branch you were on when you ran `git merge` while the second parent is the branch that was merged in.

#### The `git reset` Command
The `git reset` command is used to reset (erase) commits:

```
$ git reset <reference-to-commit>
```

It can be used to:
-   move the HEAD and current branch pointer to the referenced commit
-   erase commits
-   move committed changes to the staging index
-   unstage committed changes

#### Git Reset's Flags
The way that Git determines if it erases, stages previously committed changes, or unstages previously committed changes is by the flag that's used. The flags are:
-   `--mixed`  (default) / moving the changes we made with the commit to _Working Directory_
-   `--soft` moving the changes we made to _Staging Index_
-   `--hard` throws out all of the changes that were made in the commit

## Create a .gitignore
Create a file named _.gitignore_ and input the names of all the files and directories you want to ignore. Specifies intentionally untracked files to ignore.  
Best practice is to create .gitignore at the begining of the project. 

The `git rm -r -–cached` removes a file from the staging area. The files from the working directory will remain intact. This means that you’ll still have a copy of the file locally. The file will be removed from the index tracking your Git project.

```
# Add all the files of a folder to .gitignore. For example, a folder containing auto-#generated files

my_folder/*
```

# Git Tags
**Tags** let you point out particular commits to make them stand out from others. 
We can label the tag with: `$ git tag -a v1.0`

> CAREFUL: In the command above (`git tag -a v1.0`) the `-a` flag is used. This flag tells Git to create an _annotated_ flag. If you don't provide the flag (i.e. `git tag v1.0`) then it'll create what's called a _lightweight_ tag.

> Annotated tags are recommended because they include a lot of extra information such as:
> 
> -   the person who made the tag
> -   the date the tag was made
> -   a message for the tag

> Because of this, you should always use annotated tags.

If you type out just `$ git tag`, it will display all tags that are in the repository.

What if you accidentally misspelled something in the tag's message, or mistyped the actual tag name (`v0.1` instead of `v1.0`). How could you fix this? The easiest way is just to delete the tag and make a new one.

A Git tag can be deleted with the `-d` flag (for _delete_!) and the name of the tag:

```
$ git tag -d v1.0
```


# Git Branches
- Git branches are a way to create separate development paths without overriding or creating copies of your project
- Separate different end goals of your project
- Branches can be added, deleted and merged, just like regular commits

Branches can be used to sort of break off of the normal commit timeline and create a series of commits on a different timeline without having to mix them up with their already existing timeline your master branch.

The `HEAD` pointer points to the _branch_ that is active.

List all branches: `$ git branch -a`

You can create a branch to a previous commit using its SHA:  `$ git branch sidebar 5bfe5e7`

As you've hopefully learned by now, the `git log` command is pretty powerful and _can_ show us this information. We'll use the new `--graph` and `--all` flags. 
```
$ git log --oneline --decorate --graph --all
```
The `--graph` flag adds the bullets and lines to the leftmost part of the output. This shows the actual _branching_ that's happening. The `--all` flag is what displays _all_ of the branches in the repository.

## Merge Branches
Combining branches together is called **merging**. Git can automatically merge the changes on different branches together. This branching and merging ability is what makes Git _incredibly powerful_! You can make small or extensive changes on branches, and then just use Git to combine those changes together.

#### The Merge Command
The `git merge` command is used to combine Git branches:

```
$ git merge <name-of-branch-to-merge-in>
```

When a merge happens, Git will:
-   look at the branches that it's going to merge
-   look back along the branch's history to find a single commit that _both_ branches have in their commit history
-   combine the lines of code that were changed on the separate branches together
-   makes a commit to record the merge

To merge in the `sidebar` branch, make sure you're on the `master` branch and run:

```
$ git merge sidebar
```

Because this combines two divergent branches, a commit is going to be made. And when a commit is made, a commit message needs to be supplied. Since this is a _merge commit_ a default message is already supplied. You can change the message if you want, but it's common practice to use the default merge commit message. So when your code editor opens with the message, just close it again and accept that commit message.

#### Fast-forward Merge
In our project, I've checked out the `master` branch and I want _it_ to have the changes that are on the `footer` branch. If I wanted to verbalize this, I could say this is - "I want to merge in the `footer` branch". That "merge in" is important; when a merge is performed, the _other_ branch's changes are brought into the branch that's currently checked out.

Let me stress that again - When we merge, we're merging some other branch into the current (checked-out) branch. We're not merging two branches into a new branch. We're not merging the current branch into the other branch.

Now, since `footer` is directly ahead of `master`, this merge is one of the easiest merges to do. Merging `footer` into `master` will cause a **Fast-forward merge**. A Fast-forward merge will just move the currently checked out branch _forward_ until it points to the same commit that the other branch (in this case, `footer`) is pointing to.

To merge in the `footer` branch, run:

```
$ git merge footer
```

### Sometimes Merges Fail
Most of the time Git will be able to merge branches together without any problem. However, there are instances when a merge cannot be _fully_ performed automatically. When a merge fails, it's called a **merge conflict**.

If a merge conflict does occur, Git will try to combine as much as it can, but then it will leave special markers (e.g. `>>>` and `<<<`) that tell you where you (yep, you the programmer!) needs to manually fix.

#### What Causes A Merge Conflict
As you've learned, Git tracks _lines_ in files. A merge conflict will happen when _the exact same line(s)_ are changed in separate branches. For example, if you're on a `alternate-sidebar-style` branch and change the sidebar's heading to "About Me" but then on a different branch and change the sidebar's heading to "Information About Me", which heading should Git choose? You've changed the heading on both branches, so there's no way Git will know which one you actually want to keep. And it sure isn't going to just randomly pick for you!


# Using Git Remotely
Connect a remote repository to a local one.

In Git,  __origin__ is a shorthand name for the remote repository that a project was originally cloned from. More precisely, it is used instead of that original repository's URL - and thereby makes referencing much easier. 
In other words `origin` is an **alias** _on your system_ for a particular remote repository. It's not actually a property of that repository.

Note that origin is by no means a "magical" name, but just a standard convention. Although it makes sense to leave this convention untouched, you could perfectly rename it without losing any functionality.

In the following example, the URL parameter to the "clone" command becomes the "origin" for the cloned local repository:

```
git clone https://github.com/gittower/git-crash-course.git
```

After `git init` we add an _origin_ to the GitHub repository and allows us to connect from the local repo to the remote repo. Run `$ git remote add origin <HTML>`

By doing

```
git push origin branchname
```

you're saying to push to the `origin` repository. There's no requirement to name the remote repository `origin`: in fact the same repository could have a different alias for another developer.

Remotes are simply an **alias** that store the URL of repositories. You can see what URL belongs to each remote by using

```
git remote -v
```

In the `push` command, you can use _remotes_ or you can simply use a _URL_ directly. An example that uses the URL:

```
git push git@github.com:git/git.git master
```


## Push and Pull System
Example:
`$ git remote -v`
>origin https://github.com/somepath/repo.git (fetch)
>origin https://github.com/somepath/repo.git (push)

The first one (fetch) is the repo for pulling.
The second one (push) is the repo for pushing.


# Git Cheat-Sheet Commands
_A list of my commonly used Git commands_

### Getting & Creating Projects

| Command | Description |
| ------- | ----------- |
| `git init` | Initialize a local Git repository |
| `git clone ssh://git@github.com/[username]/[repository-name].git` | Create a local copy of a remote repository |

### Basic Snapshotting

| Command | Description |
| ------- | ----------- |
| `git status` | Check status |
| `git add [file-name.txt]` | Add a file to the staging area |
| `git add -A` | Add all new and changed files to the staging area |
| `git commit -m "[commit message]"` | Commit changes |
| `git rm -r [file-name.txt]` | Remove a file (or folder) |

### Branching & Merging

| Command | Description |
| ------- | ----------- |
| `git branch` | List branches (the asterisk denotes the current branch) |
| `git branch -a` | List all branches (local and remote) |
| `git branch [branch name]` | Create a new branch |
| `git branch -d [branch name]` | Delete a branch |
| `git push origin --delete [branch name]` | Delete a remote branch |
| `git checkout -b [branch name]` | Create a new branch and switch to it |
| `git checkout -b [branch name] origin/[branch name]` | Clone a remote branch and switch to it |
| `git branch -m [old branch name] [new branch name]` | Rename a local branch |
| `git checkout [branch name]` | Switch to a branch |
|`git checkout [commit ID]`| Goes _back in time_ to a previous commit|
| `git checkout -` | Switch to the branch last checked out |
| `git checkout -- [file-name.txt]` | Discard changes to a file |
| `git merge [branch name]` | Merge a branch into the active branch |
| `git merge [source branch] [target branch]` | Merge a branch into a target branch |
| `git stash` | Stash changes in a dirty working directory |
| `git stash clear` | Remove all stashed entries |

### Sharing & Updating Projects

| Command | Description |
| ------- | ----------- |
| `git push origin [branch name]` | Push a branch to your remote repository |
| `git push -u origin [branch name]` | Push changes to remote repository (and remember the branch) |
| `git push` | Push changes to remote repository (remembered branch) |
| `git push origin --delete [branch name]` | Delete a remote branch |
| `git pull` | Update local repository to the newest commit |
| `git pull origin [branch name]` | Pull changes from remote repository |
| `git remote add origin ssh://git@github.com/[username]/[repository-name].git` | Add a remote repository |
| `git remote set-url origin ssh://git@github.com/[username]/[repository-name].git` | Set a repository's origin branch to SSH |

### Inspection & Comparison

| Command | Description |
| ------- | ----------- |
| `git log` | View changes |
| `git log --summary` | View changes (detailed) |
| `git log --oneline` | View changes (briefly) |
| `git diff [source branch] [target branch]` | Preview changes before merging |
