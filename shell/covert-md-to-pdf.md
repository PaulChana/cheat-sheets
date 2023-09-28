# Convert md to pdf

First install the packages needed

```sh
brew install pandoc
brew install basictex
```

Then...

```sh
pandoc -f markdown-implicit_figures -t pdf INPUT_MARKDOWN > OUTPUT_PDF
```

#shell 