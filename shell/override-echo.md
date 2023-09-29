# Override echo

```sh
run_mode=debug

echo () 
{
	[[ "$run_mode" ]] && builtin echo $@
}
```

#shell 