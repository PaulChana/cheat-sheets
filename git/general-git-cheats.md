# Git cheats

## Find root directory

```sh
git rev-parse --show-toplevel
```

## Remove mis-commited files

```sh
git reset <previous label or sha1>
git commit -am "blabla"
git push -f <remote-name> <branch-name>
```

## Retrieve mis-commits to HEAD

```sh
git merge HEAD@{1}
```

## Get SHA for current

```sh
git rev-parse HEAD
```

## Get branch name

```sh
git rev-parse --abbrev-ref HEAD
```

## Ignore *.orig files during a merge

```sh
git config --global mergetool.keepBackup false
```

## Reset branch to match origin

```sh
git fetch origin
git reset --hard origin/master
```

## Count commits

```sh
git log start_sha..end_sha --pretty=oneline | wc -l
```

## Interactive rebase over a number of commits

```sh
git rebase -i HEAD~54 # (where 54 is the count)
```

## Make sublime (or equivalent) the editor

```sh
sudo ln -s /Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl /usr/local/bin/sublime
git config --global core.editor "sublime -n -w"
```

## Make Beyond compare (or equivalent) the editor

```sh
# Launch Beyond Compare, go to the Beyond Compare menu and run Install Command Line Tools.

# Diff
git config --global diff.tool bc3

# To launch a diff using Beyond Compare, use the command:
# git difftool file.ext

# Merge Pro only
git config --global merge.tool bc3
git config --global mergetool.bc3.trustExitCode true

# To launch a 3-way merge using Beyond Compare, use the command:  
# git mergetool file.ext
```

## Commits since a tag

```sh
git log --pretty=format:%s <TAG>..HEAD
```

## List all submodules

```sh
grep path .gitmodules | sed 's/.*= //'
```

## Checkout branch and track remote

```sh
git checkout -b feature/project --track origin/feature/project
```

## Show all local branches with your current branch starred

```sh
git branch
```

## Are we up to date with remote

```sg
git status -uno
```

## Add all files and commit

```sh
git add -A && git commit -m "Your Message"
```

## Commit add push

```sh
git add -A && git commit -m "Project update" && git push -u origin master
```

## Add with checks for the hunks

```sh
git add -p
```

## Add all and commit and push

```sh
git commit -am "Message" && git push
```

## Create and push branch

```sh
git checkout -b develop
git push -u origin develop
```

## Pull a repo

```sh
git pull --recurse-submodules --no-commit --rebase
```

## Delete a tag from origin

```sh
git tag -d 0.1.3
git push origin :refs/tags/0.1.3
```

## Last tag on a branch

```sh
git describe --abbrev=0 --tag
```

## Replace entire folder with one from another branch

```sh
git rm -r /path/to/folder
git checkout OTHER_BRANCH -- /path/to/folder
```

## See file history

```sh
git log -p <FILENAME>
```

## Show contents of a stash

```sh
git stash show -p
```

## Get date of all tags

```sh
git log --tags --simplify-by-decoration --pretty="format:%ci %d"
```

#git