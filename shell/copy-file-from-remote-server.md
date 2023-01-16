# Copy file from remote server to clipboard

```sh
ssh -p PORT IP "cat FILEPATH" | pbcopy
```

# Copy file from remote server to local file

```sh
scp -P PORT IP:/path/to/file .
```

#shell 