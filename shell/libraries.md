# Library tools

## See SDK type in static library

```sh
otool -lv static-lib.a
```

## Get the arch from a static library

```sh
lipo -info static-lib.a 
```

## Combine static libraries for form a fat binary

```sh
lipo -create libname_armv6.a libname_armv7.a libname_i368.a -output libname.a
```

#shell #libraries