# Combine static libraries for form a fat binary

```sh
lipo -create libname_armv6.a libname_armv7.a libname_i368.a -output libname.a
```

#shell #libraries