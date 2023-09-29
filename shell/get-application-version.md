# Get application version

```sh
function get_application_version ()
{
    local path_to_application=$1
    local the_version=$(\
    /usr/libexec/PlistBuddy -c 'Print CFBundleShortVersionString'\
    "$path_to_application"/Contents/Info.plist\
    )
    echo "$the_version"
}
```

#shell #macos