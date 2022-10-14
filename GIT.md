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

### Difference
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

### Git Revert & Reset
Git **Revert** is a little bit safer. It goes back in time to only one commit. It looks at this commit and reverse the changes and then creates a new commit saying tha it reverted the changes. 
Usage: `git revert [commit ID]`

Git **Reset** is the more dangerous option.
- **Soft**
	- Using the `--soft` flag will change your commit, but will not remove any of the changes you have made.
	- For example, if you reset back one commit, your environment would be the same, but the commit you are on would be changed.
	- This is useful if you are trying to get rid of a problem with the commit (eg. Spelling error).
- 




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
