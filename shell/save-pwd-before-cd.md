# Save $PWD before cd

```
pushd . >/dev/null
cd <PATH>
# ... Do stuff!
popd . >/dev/null
```

#shell