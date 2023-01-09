# Code signing & Notarization

## Extract certificates from application and print to stdout

```sh
#!/bin/bash

mkdir signing-certs
cd signing-certs
codesign -dvvvv --extract-certificates "$1"
openssl x509 -inform DER -in codesign0 -text
cd ../
rm -rf signing-certs
```

## Validate code signing (spctl)

```sh
spctl —assess —type execute
```

## Validate code signing (codesign)

```sh
codesign -vv —deep /Path/To/Application.app
```

## Validate signature (spctl -> gatekeeper verbose)

```sh
spctl -a -t exec -vv /Path/To/Application.app

# The output will look something like:
# <code-path>: accepted
# source=Developer ID
# origin=<identity>
```

## Validate DMG signature

```sh
spctl -a -t open --context context:primary-signature -v /Path/To/DMG.dmg
```

## Validate PKG signature

```sh
spctl -a -vv -t install /Path/to/PKG.pkg
```

## See PKG signature

```sh
pkgutil --check-signature /Path/to/PKG.pkg
```

## See application signature

```sh
codesign -dv —verbose=4 /Path/To/Application.app
```

## See information about signature of application

```sh
codesign -d -r- /Path/To/Application.app
```

## View result of notarization using altool

```sh
xcrun altool --notarization-info <build-uuid-from-altool-run> -u "<email>" -p "@env:PASSWORD_HERE"
```

## View notarization history using altool

```sh
xcrun altool --notarization-history 0 -u "<email>" -p "@env:PASSWORD_HERE"
```

#shell #codesigning