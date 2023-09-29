# Trap signals

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

#shell 