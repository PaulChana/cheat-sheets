# List remotes that haven't been committed to since...

```sh
git for-each-ref --format='%(refname:short) %(committerdate)' refs/remotes/origin | while read branch date; do
    if [[ "$(git log -n 1 --since='6 months ago' --pretty=format:"%at" "$branch")" == "" ]]; then
        echo "$branch"
    fi
done
```

#git