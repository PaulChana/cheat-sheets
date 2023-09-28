# See common name of p12 encoded cert

```sh
openssl pkcs12 -in <file.p12> -nodes -passin pass:<password> | openssl x509 -noout -subject | awk -F'[=/]' '{print $6}'`.strip`
```

#bash #codesigning 