# How to measure zsh startup time

## Show startup time

```sh
time  zsh -i -c exit
```

## Profile startup

```sh
# At top of ~/.zshrc
zmodload zsh/zprof

# At end of ~/.zshrc
zprof
```

#shell 