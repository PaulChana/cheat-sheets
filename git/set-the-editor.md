## Make sublime (or equivalent) the editor

```sh
sudo ln -s /Applications/Sublime\ Text\ 2.app/Contents/SharedSupport/bin/subl /usr/local/bin/sublime
git config --global core.editor "sublime -n -w"
```

#git