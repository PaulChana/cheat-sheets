# Notarization using altool
## View result of notarization

```sh
xcrun altool --notarization-info <build-uuid-from-altool-run> -u "<email>" -p "@env:PASSWORD_HERE"
```

## View notarization history

```sh
xcrun altool --notarization-history 0 -u "<email>" -p "@env:PASSWORD_HERE"
```

#shell #codesigning