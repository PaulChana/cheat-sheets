# Git submodule cheats

## Remove a submodule

```sh
# Delete the relevant section from the .gitmodules file.
# Stage the .gitmodules changes git add .gitmodules
# Delete the relevant section from .git/config.
git rm —-cached path_to_submodule # (no trailing slash).
rm -rf .git/modules/path_to_submodule # (no trailing slash).
git commit -m “Removed submodule “
# Delete the now untracked submodule files 
rm -rf path_to_submodule
```

## Add a submodule

```sh
git submodule add <PATH>
```

## Move a submodule

```sh
git mv old/submodule new/submodule
```

## Recursive update of submodules

```sh
git submodule update --init --recursive
````

## List submodules

```sh
grep path .gitmodules | sed 's/.*= //'
```

#git