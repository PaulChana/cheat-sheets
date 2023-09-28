# Check if bash is above a specific version

```sh
[ "${BASH_VERSINFO:-0}" -ge 4 ] && echo "yep, its at least v4"
```

#shell 