# Validate code signing using spctl
```sh
spctl -a -t exec -vv /Path/To/Application.app

# The output will look something like:
# <code-path>: accepted
# source=Developer ID
# origin=<identity>
```

#shell #codesigning 