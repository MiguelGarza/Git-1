# Workflow

1. [First time](#first-time)
    - [Initialize](#initialize)
    - [Clone](#clone)
1. [Working with changes](#working-with-changes)
1. [Check your status](#check-your-status)
1. [Sync with remote](#sync-with-remote)

## Timeline

```
Init or clone
     \
      \
    Make changes -> Stage them -> Commit them
         \                            /
          -- <- Sync with remote <- --
```

## First time

You need to do this only once every time you want to work on a new repository. There are two options:

1. **Initialize** a repository
1. **Clone** a repository

### Initialize

You would want to initialize a repo when you are going to **start from scratch**. To do this, start a project, an app, an empty folder, or whatever you want with the *IDE*, *editor* or *framework* you want.

Once you are in your workspace folder, use the `init` command.

```bash
git init
```

> This command will only work when your directory does **NOT** have a repo already

### Clone

Use this when you have a repo created, maybe by yourself or you are going to work on the repo of someone else, or you want to add changes to a repo that you started on another computer.

Go to the location where the remote repo is stored, usually **GitHub**, then copy its URL or SSH dir.

```bash
git clone <address>
```

For example, using an URL

```bash
git clone https://github.com/CesarJZO/Git.git
```

Or using the SSH protocol

```bash
git clone git@github.com:CesarJZO/Git.git
```

## Working with changes

At this point you are going to do this quite often. Just follow this principle:

1. Make changes as normal (write some code, add, modify, delete...)

2. Add those changes to the staging area

```bash
git add <files_set>
```

3. Commit changes

```bash
git commit
```

You will **always** be doing this three steps, no matter you are working alone or with a team, changing a single variable or refactoring the entire project.

## Check your status

Before you make commits and before you publish them, you may want to know what the fuck you have been doing during your code session, check your progress with these two commands

Use `log` to check you commit history, I usually add `--oneline` to get a list of one line for each commit and `--graph` when I work with branches to see how are they managed, but those two are completely optional

```bash
git log --oneline --graph
```

You can check your *current status* using `status`, this will show what files have been modified, added or deleted, also which are staged and it will compare your local branch with your remote branch (normally your local against GitHub)

```bash
git status
```

## Sync with remote

When you have a remote repo and start working on your machine, there may be changes you need to have before you send your own changes, so follow these steps

1. Check if there are changes you don't have

```bash
git fetch
```

2. Before `commit` your own changes or before making any, `pull` the changes stored on the remote repo

```bash
git pull
```

3. Now, work as normal, maybe resolve some **merge conflicts**, and after you `commit`ted everything you want to publish to your **remote branch**, `push` your changes to be stored on your remote repo

```bash
git push
```

If it's the first time you are going to `push` changes, use the `-u` flag to set the upstream branch

```bash
git push -u <remote_name> <branch>
```

For example

```bash
git push -u origin main
```
