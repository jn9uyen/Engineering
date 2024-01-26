# GIT Notes

## [Configure user name and email (global)](https://support.atlassian.com/bitbucket-cloud/docs/configure-your-dvcs-username-for-commits/)
```
git config --global user.name "jnguyen-dev-1"
git config --global user.email "jnguyen11@woolworths.com.au"
```

## Store credentials on local machine
```
git config --global credential.helper store
```
**Warning**: If you use this method, your Git account passwords will be saved in plaintext format, in the global .gitconfig file, e.g in Linux it will be `~/.gitconfig` (view using `cat ~/.gitconfig`). If this is undesirable to you, use an ssh key for your accounts instead. [link](https://stackoverflow.com/questions/35942754/how-can-i-save-username-and-password-in-git)


## [Create local repo and add remote](https://www.atlassian.com/git/tutorials/setting-up-a-repository)
1. Initialise local repo
```
cd /path/to/your/existing/code
git init
```
2. Add files and commit files
```
git add .
git commit -m "first commit"
```
3. Link remote repo
```
git remote add <remote_name> <remote_repo_url>
e.g. git remote add origin <remote_repo_url>
```
4. If files exist on remote:
a. specify branch to pull from: e.g. 
```
git pull origin master
```
b. set it up so that your local master branch tracks github master branch as an upstream
```
git branch --set-upstream-to=origin/master master
git pull
```
c. trouble with unrelated histories: solution:
```
git pull origin master --allow-unrelated-histories
```
5. Push to remote
```
git push -u <remote_name> <local_branch_name>
git push -u origin master
```

## Better Solution to above (clone from remote):
```
git clone https://github.com/roparzhhemon/myremoterepo.git
```
then add files, commit, push

## [Steps to create a new local branch](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches)
1. Before creating a new branch, pull the changes from upstream. Your master needs to be up to date.
```
git pull
```

2. Create the branch on your local machine and switch to this branch:
```
git checkout -b <new_branch>
```

3. Rebase to origin/develop (not need if step 1 has been done)
```
git pull --rebase origin develop
```

4. For the first push to remote, use the -u flag (upstream) to track:
https://www.freecodecamp.org/forum/t/push-a-new-local-branch-to-a-remote-git-repository-and-track-it-too/13222
```
git push -u origin <branch>
```

## Rebase options
```
git rebase --edit
git rebase --skip
git rebase --abort
```

## View branches
```
git branch     # local branches
git branch -r  # remote branches
git branch -a  # all
```

### Remove remotely-deleted branches that appear in local `git branch -a`
```
git remote prune origin
```

## Change / swtich branch
```
git checkout <existing_branch>
```

## Create branch
```
git checkout -b <new_branch>
git pull --rebase <remote> (e.g. origin develop)
```

## Create branch from another branch (e.g. develop)
```
git checkout -b <new_branch> <other branch>
```

### Create orphan branch
```
git checkout --orphan <new_branch>
```
The core use for `git checkout --orphan` is to create a branch in a `git init`-like state on a non-new repository. A situation is where you want to keep the files from a certain branch and truncate the history of your repository.

## [Delete branch](https://www.educative.io/edpresso/how-to-delete-remote-branches-in-git)
```
git branch -d <branch>
git branch -D <branch> # force delete
git push origin --delete <branch> # delete on repo
```

## View commits
```
git log --oneline
```

## Rollback to particular commit
```
git reset --hard <tag/branch/commit id>
```

## Unstage local commits (n == number of commits)
```
git reset --soft HEAD~n
# e.g. 2 commits to unstage:
git reset --soft HEAD~2
```

## Add changes to previous commit: rollback and amend
```
git reset HEAD~ 
git commit --amend
```

## Force push
```
git push -f
git reset --hard <sha1-commit-id>
```

## Delete commit: move `HEAD` pointer to the `sha1-commit-id`
```
git reset --hard <sha1-commit-id>
```

## Stash (-m for message)
```
git stash -m 
```

#### [Show stash](https://git-scm.com/docs/git-stash)
```
git stash show
git stash list
```

### Reapply stash (throw away stash)
```
git stash pop

# retain stash in stash
git stash apply
```

### Show stash changes (+-)
```
git stash show -p
```

### Remove git stash
```
git stash drop
git stash drop@{n}
# e.g.
git stash drop 1
```
where n is the number shown from `git stash list`

## Remove untracked from local
### 1. Display files to remove
```
git clean -n
```
### 2. Remove files
```
git clean -f
```
