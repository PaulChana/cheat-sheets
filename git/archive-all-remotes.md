# Archive all remotes

```bash
#!/bin/bash

BRANCHES=("<BRANCH_NAME1>" "<BRANCH_NAME2>" "<BRANCH_NAME3>")
ROOT_DIRECTORY="<PATH TO WHERE TO WRITE>"
GIT_DIRECTORY="<PATH TO GIT LOCATION>"

pushd . >/dev/null

cd "$GIT_DIRECTORY" || exit

for BRANCH in "${BRANCHES[@]}"; do

    BRANCH_DIRECTORY=$(dirname "$BRANCH")
    OUT_DIRECTORY=$ROOT_DIRECTORY/$BRANCH_DIRECTORY
    ZIP_TARGET=$ROOT_DIRECTORY/$BRANCH.zip

    echo "$BRANCH will be written to $OUT_DIRECTORY as $ZIP_TARGET"

    mkdir -p "$OUT_DIRECTORY"
    git archive --format zip --output "$ZIP_TARGET" "$BRANCH"

done

popd . >/dev/null
```

#git