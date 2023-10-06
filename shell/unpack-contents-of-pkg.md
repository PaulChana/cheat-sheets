# # Unpack installable files from a PKG

```sh
mkdir foo
cd foo
xar -xf ../foo.pkg
cd foo.pkg
cat Payload | gunzip -dc |cpio -i
```

#shell #pkg