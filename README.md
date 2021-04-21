# Git "tips"

This repository contains some tips for `git`.

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

Auto update:

```bash
$ less ~/.zshrc
...
DISABLE_UPDATE_PROMPT="true"
...
```

[Plugins](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins):

```bash
$ less ~/.zshrc
...
plugins=(git ripgrep)
...
```

Git commands:

| Short | Command |
| ----- | ------- |
| gst   | git status |
| ga    | git add |
| gco   | git checkout |
| gd    | git diff |
| gdw   | git diff --word-diff |
| gdca  | git diff --cached |
| gdcw  | git diff --cached --word-diff |

# Git global hooks - git 2.9+

Pre-push script: [pre-push](./my-git-hooks/hooks/pre-push) - will warn if pushing to protected branch, script below:

```bash
#!/usr/bin/env bash
# Warn before pushing to protected branches
# Make script executable with chmod +x pre-push
# Bypass with git push --no-verify
# Change default git hooks:
# git config --global core.hooksPath /path/to/my/centralized/hooks
BRANCH=$(git rev-parse --abbrev-ref HEAD)
PROTECTED_BRANCHES="^(master|dev|release-*|patch-*)"
if [[ "$BRANCH" =~ $PROTECTED_BRANCHES ]]; then
  read -p "[LOG] Are you sure you want to push to \"$BRANCH\" ? (y/n): " -n 1 -r < /dev/tty
  echo
  if [[ $REPLY =~ ^[Yy]$ ]]; then
    exit 0
  fi
  echo "[ERR] Push aborted."
  exit 1
fi
exit 0
```

Download and enable **global hooks**:

```
cd ~
mkdir -p ~/.my-git-hooks/hooks
wget 'https://raw.githubusercontent.com/kaczla/git-tips/master/my-git-hooks/hooks/pre-push' -O ~/.my-git-hooks/hooks/pre-push
chmod u+x ~/.my-git-hooks/hooks/pre-push
git config --global core.hooksPath "$(realpath ~)/.my-git-hooks/hooks"
cd -
```

Now, **global hooks** should be enabled, to check run command:

```bash
$ git config --get core.hookspath
/home/MY_USER_NAME/.my-git-hooks/hooks
```

# English messages

Add alias in Shell RC file (bash - `.bashrc`, zsh - `.zshrc`):

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

Rebase current branch in **interactive** mode (example 1):

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
git diff master..diff-me
```

Comparing 2 non-git files: **1.txt** and **2.txt**:

```bash
git diff --no-index --word-index 1.txt 2.txt
```

shorter:

```
gdw --no-index 1.txt 2.txt
```

Comparing 2 non-git directories **dir1** and **dir2**:

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

Stash uncommited changes:

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

- Example 1 - remove empty commit using `git rebase -i`
 - read [README](./EXAMPLE_1.md) for details
 - branch [rebase_interactive](https://github.com/kaczla/git-tips/tree/rebase_interactive)
