# Git "tips"

This repository contains some tips for `git`.

Ad some message in README.

# Oh My Zsh

[Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh) is an open source, community-driven framework for managing your zsh configuration.

Installation **zsh**:

Ubuntu:

```bash
$ sudo apt-get install zsh
```

Arch Linux:

```bash
$ sudo pacman -S zsh
```

Installation **Oh My Zsh**:

```bash
$ sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
$ chsh -s $(which zsh)
```

Enable auto updates - set `DISABLE_UPDATE_PROMPT` to `true`:

```bash
$ less ~/.zshrc
...
DISABLE_UPDATE_PROMPT="true"
...
```

[Plugins](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins) (see GitHub wiki for more plugins) can be activated in `plugins` sections:

```bash
$ less ~/.zshrc
...
plugins=(git ripgrep)
...
```

See other plugins:
[git](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git),
[ripgrep](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/rg),
[python](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/python),
[pip](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/pip),
[rust](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/rust),
[docker](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/docker),
[docker-compose](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/docker-compose)

Git commands/aliases with Oh My Zsh [git](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/git) plugin:

| Short | Command |
| ----- | ------- |
| g     | git |
| gst   | git status |
| ga    | git add |
| gco   | git checkout |
| gd    | git diff |
| gdw   | git diff --word-diff |
| gdca  | git diff --cached |
| gdcw  | git diff --cached --word-diff |

# Git global hooks - git 2.9+

Pre-push script: `pre-push` - will warn if pushing to protected branch, script is available in [GitHub repository](https://github.com/kaczla/git-hooks).

# English messages

To enable english messages add alias in Shell RC file (bash - `.bashrc`, zsh - `.zshrc`) at the end of the file (to avoid anomalies):

```bash
alias git='LANGUAGE=en_US.UTF-8 git'
```

# Custom aliases

```bash
alias git_compare_word='git diff --no-index --word-diff'
alias diff_git_word='git_compare_word'
alias git_compare='git diff --no-index'
alias diff_git='git_compare'
```

# Git external tools
- [GitUI](https://github.com/Extrawurst/gitui) provides you with the comfort of a git GUI but right in your terminal

# Commands

## git commit

Pushing empty commit:

```bash
git commit -m "[pre-release] Test docker image" --alow-empty
```

Amending commit with current date:

```bash
git commit --amend --date=now
```

## git rebase

Rebase with **master** branch:

```bash
git rebase master
```

Rebase current branch in **interactive** mode ([example 1](#example-1)):

```bash
git rebase -i HEAD~3
```

## git checkout

Getting **some-file.txt** from **master** branch:

```bash
gco master -- some-file.txt
```

## git diff

Check last 2-commit changes:

```bash
git diff HEAD~2
```

or shorter:

```bash
gd HEAD~2
```

Comparing **master** and **develop** branches:

```
git diff master..develop
```

Comparing 2 **non-git** files: **1.txt** and **2.txt**:

```bash
git diff --no-index --word-index 1.txt 2.txt
```

shorter:

```
gdw --no-index 1.txt 2.txt
```

Comparing 2 **non-git** directories **dir1** and **dir2**:

```bash
git diff --no-index dir1 dir2
```

shorter:

```bash
gd --no-index dir1 dir2
```

Comparing changes with context (only changes will be available - context may be changed by **U** argument):

```bash
git diff -U0
```

Comparing only deleted changes:

```bash
git diff --diff-filter=d
```

## git log

One line commits:

```bash
git log --oneline
```

## git stash

Stash uncommitted changes:

```bash
git stash
```

Pop stashed changes:

```bash
git stash pop
```

List stashed changes:

```bash
git stash list
```

Drop stashed changes (stashed changes are indexed from 0)

```bash
git stash drop stash@{0}
```

or remove all:

```bash
git stash clear
```

## git grep

Search with **grep** in **git**:

```bash
git grep 'my_secret_password'
```

# Examples

## Example 1
- Example 1 - remove empty commit using `git rebase -i`
 - read [README](./EXAMPLE_1.md) for details
 - branch [rebase_interactive](https://github.com/kaczla/git-tips/tree/rebase_interactive)
