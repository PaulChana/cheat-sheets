# Create a new GitHub SSH key

This comes from [here](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

```sh
ssh-keygen -t rsa -b 4096 -C "github email address here"
```

When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.

#git #github