## Version Control - GIT

---

- git init: Initializes a new Git repository.
  Example: `git init`

- git clone: Creates a copy of a remote repository on your local machine.
  Example: `git clone https://github.com/username/repo.git`

- git add: Adds changes to the staging area.
  Example: `git add .`

- git commit: Creates a new commit with the changes in the staging area.
  Example: `git commit -m "Initial commit"`

- git status: Shows the status of the working directory, including changes that have been made but not yet committed.
  Example: `git status`

- git log: Shows the commit history of the repository.
  Example: `git log`

- git diff: Shows the differences between the working directory and the latest commit.
  Example: `git diff`

- git branch: Shows the branches in the repository.
  Example: `git branch`

- git branch <branch_name>: Creates a new branch with the given name.
  Example: `git branch new_feature`

- git branch -d <branch_name>: Deletes the specified branch.
  Example: `git branch -d new_feature`

- git checkout <branch_name>: Switches to the specified branch.
  Example: `git checkout new_feature`

- git merge <branch_name>: Merges the specified branch into the current branch.
  Example: `git merge new_feature`

- git pull: Fetches changes from a remote repository and merges them into the current branch.
  Example: `git pull origin master`

- git push: Pushes commits to a remote repository.
  Example: `git push origin master`

- git stash: Temporarily saves changes that have not been committed.
  Example: `git stash`

- git stash pop: Restores the most recently stashed changes.
  Example: `git stash pop`

- git rebase <branch_name>: Integrates changes from the specified branch into the current branch, by reapplying the current branch's commits on top of the specified branch's commits.
  Example: `git rebase master`

- git reset <commit_hash>: Undoes commits, moving the HEAD and branch pointer to the specified commit. This command discards commits, destroying the commits and the changes that were made in those commits.
  Example: `git reset abc123`

- git revert <commit_hash>: Undoes commits, by creating new commits that revert the changes made in the specified commit. This command keeps the commits and the history intact and creates new commits that cancel out the changes made in the specified commit.
  Example: `git revert abc123`

- git cherry-pick <commit_hash>: Applies the changes made in the specified commit to the current branch. This command allows you to selectively apply specific commits from one branch to another, rather than merging an entire branch.
  Example: `git cherry-pick abc123`
