# Access notarization log file

```sh
xcrun notarytool log CREDENTIALS REQUEST_UUID > notary.log
```

`REQUEST_UUID` will come from the request and is likely written to a log file
`CREDENTIALS` will be `--keychain-profile "AC_PASSWORD"` assuming you are using the keychain

#codesigning #shell 