# Extract certificates from application and print to stdout

```sh
#!/bin/bash

mkdir signing-certs
cd signing-certs
codesign -dvvvv --extract-certificates "$1"
openssl x509 -inform DER -in codesign0 -text
cd ../
rm -rf signing-certs
```

#shell #codesigning  