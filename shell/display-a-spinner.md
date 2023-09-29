# Display a spinner

```sh
spinner="/-\|"
index=1

printf "\b${spinner:index++%${#spinner}:1}"
```

#shell 