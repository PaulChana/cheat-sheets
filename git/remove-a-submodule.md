# Remove a submodule

```sh
# Delete the relevant section from the .gitmodules file
# Stage the .gitmodules changes 
git add .gitmodules
# Delete the relevant section from .git/config
git rm --cached path_to_submodule # (no trailing slash)
rm -rf .git/modules/path_to_submodule # (no trailing slash)
git commit -m "Removed submodule "
# Delete the now untracked submodule files 
rm -rf path_to_submodule
```


# Remove a submodule as a script

```sh
#!/bin/bash

# Check if the user provided a submodule path
if [ -z "$1" ]; then
  echo "Usage: $0 <submodule_path>"
  exit 1
fi

SUBMODULE_PATH=$1

# Remove the submodule entry from .gitmodules
echo "Removing submodule from .gitmodules..."
git config -f .gitmodules --remove-section "submodule.$SUBMODULE_PATH" || {
  echo "Failed to remove submodule section from .gitmodules"
  exit 1
}

# Remove the submodule's configuration from .git/config
echo "Removing submodule configuration from .git/config..."
git config -f .git/config --remove-section "submodule.$SUBMODULE_PATH" || {
  echo "Failed to remove submodule section from .git/config"
  exit 1
}

# Unstage the submodule and remove the files
echo "Removing submodule files..."
git rm --cached "$SUBMODULE_PATH" || {
  echo "Failed to unstage submodule files"
  exit 1
}

# Delete the submodule's files from the working tree
rm -rf "$SUBMODULE_PATH" || {
  echo "Failed to delete submodule files"
  exit 1
}

# Remove any leftover submodule data in .git/modules
echo "Removing leftover submodule data in .git/modules..."
rm -rf ".git/modules/$SUBMODULE_PATH" || {
  echo "Failed to remove leftover submodule data"
  exit 1
}

# Commit the changes
echo "Committing changes..."
git commit -m "Removed submodule $SUBMODULE_PATH" || {
  echo "Failed to commit submodule removal"
  exit 1
}

echo "Submodule $SUBMODULE_PATH successfully removed!"
```

#git