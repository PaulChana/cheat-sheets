# Convert tabs to spaces

```sh
function convert_tabs_to_spaces_in_file () 
{
    local base_directory=`basename $1`
    local temp_file=`mktemp -q /tmp/${base_directory}.XXXXXX`

    if [ $? -ne 0 ]; then
        echo "$0: Can't create temp file, exiting..."
        exit 1
    fi

    expand -t 4 $1 >> $temp_file
    mv $temp_file $1
}
```

#shell 