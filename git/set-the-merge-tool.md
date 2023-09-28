# Make Beyond compare (or equivalent) the editor

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

#git