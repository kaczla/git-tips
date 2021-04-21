# Example 1

Goal: remove empty commit using `git rebase -i` (in interactive mode)

# Steps

At beginning `git log` returns:

```text
commit 8da5235638614fcc02a3dfc71dbe24d170862301 (HEAD -> rebase_interactive)
Author: Name Surname <user@mail.com>
Date:   Wed Apr 21 20:37:17 2021 +0200

    Add simple JSON file

commit f1fbae9fb0e615a20ed5424b18c666c07d19d429
Author: Name Surname <user@mail.com>
Date:   Wed Apr 21 20:36:11 2021 +0200

    Some empty commit

commit e77108bd9e875de8d122c484d043f4fde99b6788
Author: Name Surname <user@mail.com>
Date:   Wed Apr 21 20:35:40 2021 +0200

    Add simple text file
```

Run `git rebase -i HEAD~3` command and remove empty commit (second commit - with "Some empty commit" message) by changing `pick` to `drop` (or to `d`) value, like this:

```text
pick e77108b Add simple text file
drop f1fbae9 Some empty commit # empty
pick 8da5235 Add simple JSON file
```

And, now `git log` returns:

```text
commit 584b4f2d80cac92bc69645cdcec8eee327b7fc83 (HEAD -> rebase_interactive_2)
Author: Name Surname <user@mail.com>
Date:   Wed Apr 21 20:37:17 2021 +0200

    Add simple JSON file

commit e77108bd9e875de8d122c484d043f4fde99b6788
Author: Name Surname <user@mail.com>
Date:   Wed Apr 21 20:35:40 2021 +0200

    Add simple text file
```

To push changes use `--force` option: `git push -f` or push into new branch.
