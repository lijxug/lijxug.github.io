---
title: How to Use Git-01
tags:
  - git
categories:
  - memo
date: 2017-07-17 19:24:44
---


# Introduction
**git** is a very useful and powerful tool for version control and team work. It's commonly used in computer field, but it can be useful in the work of other fields too. I've been used it through package developing using Rstudio for a while. Recently, in order to [auto-update this blog](https://lijxug.github.io/2017/07/13/Use-Travis-CI-for-autoupdating-GitHub-pages/), I've learned some useful git skills. That's the moment I want to write all I've learned so far down as a memo as usual and try to keep up.

<!-- more -->
Before we start, here is an useful website. 

[https://git-scm.com/](https://git-scm.com/ "all you need about git")

It contains everything you need to know about git.

# Configuration
After installation, the first thing you want to do is config your name and email address.
```
git config --global user.name "XXX"
git config --global user.email "XXX@XXX.com"
```
The option `--global` means from now on, every project on this computer will automatically use these information. If you want to have a special project that use another set of information, it can be done simply config without the option `--global`.

You can check your configuration by:
```
# all of them
git config --list 
# one fo them
git config user.name
```

# Basic Workflow
In my opinion, a basic workflow of git includes several steps:

1. Get a local repository(`git init` or `git clone`)
2. Modify the local repository.
3. Add changes(`git add`)
4. Commit them(`git commit`): a ready-to-push buffer zone
5. Push changes to the remote repository(`git push`)

## Getting a Repository

### Initializing a Repository in an Existing Directory
To start a project, you have to create a repository for it. Repository functions as a folder. Every changes happen in this folder, including adding/removing/modifying files, is tracable. 
```
mkdir test_repo && cd test_repo
git init
```

### Cloning an Existing Repository
If you are familiar with github, you will know what this is all about. If you want to work on an existing project, you have to get a copy of them from another computer or server first. 
In this case, `git clone [url]` is what you need.
```
# basic
git clone https://github.com/libgit2/libgit2.git
# clone into directory "mylibgit"
git clone https://github.com/libgit2/libgit2.git mylibgit
# clone only a branch of it
git clone -b [branch name] https://github.com/libgit2/libgit2.git
```

## Recording Changes
### Checking Status of Your Files
```
git status
# short version
git status -s
```
### Tracking Changes & Staging
```
touch README.md
# git status
git add README.md
```

{% asset_img git-add.png}

In one word, `git add .` means staged all the changes so far in your repository. But it's risky if you are not used to `git status` check your commits every time.

Now the change is staged because it's under the "Changes to be commmitted". Notice that this "staged version" is no longer your current version of file. That means, if you change your files after `git add`, you will have to `add` them again to stage the latest version.

You can use `git diff` to find more details about staged and unstaged changes:
```
# to see what you've changed but not yet staged
git diff
# to see what you've staged
git diff staged
```

### Committing Your Changes
Now that you've add some modifications in the staged bucket, it's time to commit them! 
```
# the simplest way
git commit
# add commit message inline
git commit -m "blablabla"
```

### Others
```
# untrack and delete a file
rm XXX.md
git rm XXX.md
# mv
mv XX.md XXX.md
git mv XX.md XXX.md
```

# Roll-back
## Viewing the Commit History
```
# lists the commits made in that repository in reverse chronological order
git log
# -p shows the difference introduced in each commit, -2 limits the output to only the last two entries
git log -p -2
# --pretty=oneline/short/full/fuller/format:"..."
git log --pretty=oneline
git log --pretty=format:"%h - %an, %ar : %s"
```
More details of `format` are shown here:
{% asset_img git-log-pretty-format.png}

The history of a git project could be huge and complex, please check [the manual](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History) for further information.

## Undoing Things
### `--amend`
```
git commit -m "initial commits"
git add forgotten_files
git commit --amend
```

### Reset
To unstage a file...
```
git reset HEAD <file>
```
To reset the current branch to `HEAD`
```
git reset [--hard|soft|mixed|merge|keep] [HEAD or <commit>]
```
- **--hard** 

    Reset index and working tree, any changes since `<commit>` are discarded. Danger! Be very careful about it.

- **--soft** 

    Does not touch the index file or the working tree at all (but resets the head to `<commit>`, just like all modes do). This leaves all your changed files "Changes to be committed", as git status would put it.

- **--mixed**
    Does not touch the index file or the working tree at all (but resets the head to <commit>, just like all modes do). This leaves all your changed files "Changes to be committed", as git status would put it.

```
# rollback to last edition
git reset --soft HEAD^
git reset --soft HEAD~1
```
Actually, if you know the commit id of an "future" edition, you can `reset` to it, too. `git reflog` may help you to find it. 

Please check [the manual of git-reset](https://git-scm.com/docs/git-reset) for more details.

### Unmodify
You can use `git checkout -- FILE` to unmodify a FILE.

# Getting Help

There are three ways to get the manual page for any of the Git commands:

```
git help <verb>
git <verb> --help
man git-<verb>
# for example
git help config
```

