# Shell utilities

## Combine commands

```sh
A; B    # Run A and then B, regardless of success of A
A && B  # Run B if and only if A succeeded
A || B  # Run B if and only if A failed
A &     # Run A in background.
```

## Display a spinner

```sh
spinner="/-\|"
index=1

printf "\b${spinner:index++%${#spinner}:1}"
```

## Override echo

```sh
run_mode=debug

echo () 
{
	[[ "$run_mode" ]] && builtin echo $@
}
```

## Read user input

```sh
read -p "Press any key to continue... " -n1 -s
```

## Clear the display

```sh
clear && printf '\e[3J'
```

## Round a float to an int

```sh
printf "%.0f" 2743410360.320
```

## Get terminal dimensions

```sh
tput lines # Print number of lines
tput cols  # Print number of columns
```

## Hide the cursor

```sh
tput civis
```

## Show the cursor

```sh
tput cnorm
```

## Move cursor to start of line

```sh
printf "\b\r"
```

## Compute SHA256

```sh
echo -n "simple text" | shasum -a 256
```


## Bold, underline, reverse text in terminal

```sh
tput bold # Bold text
tput smul # Underline text
tput rev  # Reverse text
```

## Simulate high CPU load

```sh
yes > /dev/null & yes > /dev/null & yes > /dev/null & yes > /dev/null &

# To stop the CPU load
killall yes
```

## Trap signals

```sh
function cleanup() 
{
    echo "Caught signal"                                                                                                                           
}

function catch_quit ()
{
    echo "Caught quit"
} 

# you can trap different things for different items
trap cleanup TERM INT 
trap catch_quit QUIT
```

## Convert tabs to spaces

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

## Get application version

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

## Repeat a command every x seconds

```sh
brew install watch
watch -n time_in_seconds <your command>
```

#shell 