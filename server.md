# Server

In this page, I will list some instructions to create a custom server for a git repository using the SSH protocol

## Setting up

First, you need a PC with any standard Linux distribution, in it, make sure to have an `.ssh` folder in your home directory (or in the user you plan to use)

### Create a user (optional)

If you want to create a specific user for this task, follow this steps

Create a user. `git` will be the username in this example

```bash
sudo adduser git
```

If you want to list all the users in your PC, use this

```bash
awk -F: '{ print $1}' /etc/passwd
```

### Register the SSH key

With the user you plan to use and using the PC you plan to use as remote, create an `.ssh` folder if you don't have already

Check if you have one

```bash
ls -a
```

If you don't, create it as follows

```bash
mkdir ~/.ssh && chmod 700 ~/.ssh
touch ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys
```

Inside the `authorized_keys` you just created, paste the ssh keys of the PCs that are going to use this remote or create them following [these steps](#create-or-get-an-ssh-key-on-your-client)

```bash
cat /tmp/id_rsa.john.pub >> ~/.ssh/authorized_keys
# or using a text editor, paste the key manually
vim authorized_keys
```

### Create or get an SSH key on your client

Using the client PC, generate a new SSH key using the `ed25519` algorithm

```bash
ssh-keygen -t ed25519
```

Your new key will be stored by default in the `.ssh` folder (stored in your home directory `~`) in the `id_ed25519.pub` file

### Create the remote Git repository

Finally, you just need to create a new repo in any directory you want. You can run `git init` with the `--bare` option to initialize the repository without a working directory, or so git says

```bash
mkdir project.git # or any name you want
cd project.git
git init --bare
```

### Add that repository as remote

Using the client PC, or the same, just in another directory, create a repository with any set of files, make a commit and push it to the remote repo we just created

Note: You can name the remote repo whatever you want, `origin` is just the standard

```bash
git init
git add .
git commit -m 'Initial commit'
# Now the real deal
# Replace this direction with the real one
git remote add origin git@url:/home/git/project.git
git push origin main
```

### Cloning your fancy new remote repo

At this point, others can clone your repo and push changes as normal

```bash
git clone git@url:/home/git/project.git
cd project
vim readme.md
git commit -am 'Fixing your shit'
git push origin main
```

## References

- [Git on the Server - Setting Up the Server](https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server)
- [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
