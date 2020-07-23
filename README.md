# Git cheatsheet
I have kept this local for a long time, why not to share it? If you find a command which is not there and helped to you resolved a git issue, please send PR.

Create existing branch from remote
```
  git checkout -b <branch> origin/<branch>
```

Replace current commit with the files currently in the directory
```
  git commit --amend -C HEAD
```

Change commit message
```
  git commit --amend
```

Take all changes to tracked files and make a commit
```
  git commit -all
```

What chnages are going to be committed
```
  git diff --cached
```

Changes files in the working tree and the last commit
```
  git diff head
```

Cleaning git -d directory , -x - untracked and ignored, -f forced (-n only shows files)
```
  git clean -dxf
```

```
git log --oneline
```

Update all remotes
```
  git fetch -all
```

Reset merge to return to the stae before merging
```
  git reset --merge
```

Remove untracked changes in the working directory
```
  git stash --keep-index
  bring back the stashed changes to the working tree
  git stash pop
```

Difference between local master and origin/master (or any other branch)
```
  git diff master origin/master
  git diff master file (on branch)
```

Git log
```
  git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
```

List branches (-a all local and remote, -r only remote branches)
```
  git branch -a
  git branch -r
```

Show status files in directories
```
  git st -u
```

Rebase on master local
```
  git rebase origin/master
```

Push new branch
```
  git push -u origin your_branch
```

git stash - store uncommited changes (clean local repo)
```
  git stash
  git stash list
  git stash apply (last stash otherwise explicitly cite which one)
  git stash drop - drop last one
  git stash clear - remove ALL
  git stash pop
  git stash push
  git stash apply SHA1 - in case you dropped the stash
```

Push branch to origin
```
  git push origin branch_name
```

Diff file between modification and the last commit
```
  git diff HEAD file
```

Force push (rewrite history, don't do if shared repo or be caution)
```
  git push origin your_branch --force
```

Keeps history visible on graph
```
  git merge --no-ff
```

Remove last commit with losing files
```
  git reset --hard HEAD~1
```

Remove the last commit with files intact
```
  git reset --soft HEAD~1
```

Track remote branch (and switch to a new one)
```
  git checkout --track -b origin/daves_branch

# if multiple remotes do

  git checkout -b branch_name remote_name/branch_name
```

Move files
```
  git mv FILE destination
```

Rebase before pushing (only commits which differ from upstream - master)
```
  git rebase -i @{u}
```

Fix conflicts during merge
```
  git mergetool
```

Commit deleted files
```
  git add -u
```

Diff any commit (example diff last commit with previous)
```
  git difftool HEAD HEAD~1
```

git diff labels
```
  git diff tag1 tag2 -- some/file/name
```

Change the last commit (=edit)
```
  git commit --amend
```

show tags (label)
```
  git tag
```

Annotated tag (not lighweight!)
```
  git tag -a v1.4 -m 'my version 1.4'
```

Lightweight tags
```
  git tag my_version
```

Delete the tag locally
```
  git tag -d my_version
  # this one delets tag my_version from the remote origin
  git push origin :refs/tags/my_version
```


Diff staged
```
  git diff --cached file
```

Squash merge to master from newstuff branch
```
  git checkout master
  git merge --squash newstuff
```

Show untracked files
```
  git ls-files --other --exclude-standard
```

Diff only files name which differs
```
  git diff --name-only master <branch>
```

Remove branch (newfeature) from origin
```
  git push origin :newfeature
```

Remove local branch
```
  git brach -d branch_name
```

Show branch with commits
```
  git show-branch
```

Show which branch was merged (be concious about squash/rebase)
```
  git branch -r --merged master | sed 's/ *origin\///' | grep -v 'master$'
```

Fetch tags
```
  git fetch -t
```

Push tag
```
  git push origin [tagname]
```

Github forked update (new upstream, then merge to master fork) - mbed as an example
```
  git remote add --track master upstream git://github.com/mbedmicro/mbed.git
  git merge upstream/master
```

Change url for upstream remote
```
  git remote set-url upstream address
```

Rename remote
```
  git remote rename origin destination
```

git (github) update fork
```
  git fetch upstream
  git merge upstream/master
  or
  git pull --rebase upstream master (preffered)
```

Revert bad rebase
```
git reflog (this displays history, check which one you want to return to)
git reset <sha> --hard
```

Show commit with sha (example 1e8e50996)
```
  git show s1e8e50996
```

Fetch a branch github (already forked)
```
  git remote add theirusername git@github.com:theirusername/reponame.git
  git fetch theirusername
  git checkout -b mynamefortheirbranch theirusername/theirbranch
```

Set tracking branch (current branch to track upstream/foo)
```
  git branch -u upstream/foo
```

Change author for the last commit
```
  git rebase -i B
  change pick to edit in the tet
  git commit --amend --author="author <email>"
  git rebase --continue

  or
  git commit --ammend --author="name <email>"
```

Fetch submodules within repository
```
  git submodule update --init --recursive
```

Clone with all submodules
```
  git clone --recursive git@address
```

Add submodule
```
  git submodule add git@address
```

Find out where the branch started from another branch
```
  git merge-base HEAD BRANCH_YOU_BRANCHED_FROM
```

To create a patch from the current master, from the SHA up to the top of HEAD, all in one patch. If you don't supply --stdout option, will create a patch for each commit
```
  git format-patch <sha> --stdout > my.patch
  # use --relative for relative paths
  # or -o for output directory
```

To apply patch (no signoff involved), neither commits
```
  git apply --check my.patch
  git apply my.patch
```

To sign off and keep the log
```
git am < my.patch
# use --directory for directory where it should be applied

# for windows, as patch/*.patch does not work, use find:
find ./patch/*.patch | xargs git am

# if there are conflicts use -3, then run git mergetool to resolve conflicts
```

Push local branch to remote branch with different branch name
```
git push origin local-name:remote-name
```

Update remote url link
```
git remote set-url origin https://github.com/USERNAME/OTHERREPOSITORY.git
```

Copy files from one repo to another with history
```
git log --pretty=email --patch-with-stat --reverse -- path/to/file_or_folder | (cd /path/to/new_repository && git am)
```

Mirror a repo to a new one (clone with all branches, tags)
```
git clone --bare old_repo.git
cd old-repo.git
git push --mirror new_repo.git
```

Find out when was a file/a folder deleted
```
git log -1 -- file/folder
```

If forced to Github PRs but there were changes, git reflog is no help, use git refs to recover. The commands create a new branch in a repo (where PR come from. Use this new branch as a new point you can reset to or just cherry pick changes from)

```
curl -u <owner> https://api.github.com/repos/<owner>/<repo>/events
curl -u <owner> -X POST -d "{\"ref\":\"refs/heads/<new-branch>\", \"sha\":\"<sha found in first step>\"}" https://api.github.com/repos/<owner>/<repo>/git/refs
```

