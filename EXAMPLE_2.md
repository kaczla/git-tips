# Example 2

Goal: override commit message and fix typo

# Steps

At beginning `git log` returns:

```text
commit f5354fef86e531bec35b25172701afa42361c58f (HEAD -> commit_amend, origin/commit_amend)
Author: Name Surname <user@mail.com>
Date:   Sun Oct 3 21:11:43 2021 +0200

    Add message in README.md

commit 88454a363c92b0198b41c86c6d6194c7ffe40d52 (origin/master, master)
Author: Name Surname <user@mail.com>
Date:   Thu Sep 30 05:50:57 2021 +0200

    Add link to Example 1
```

Fix typo in `README.md` (should be `Add` but `Ad` is - in line 5) and add file with command: `git add README.md`

Next, run `git commit --amend --date=now` and change commit message (optionally). Argument `--date=now` says: put the current date in the commit.

And, now `git log` returns (in this example commit message was changed from `Add message in README.md` to `Add new message in README.md`):

```
commit 7f548863ab7ba25967e98859c5c07164e6139ddf (HEAD -> commit_amend, origin/commit_amend)
Author: Name Surname <user@mail.com>
Date:   Sun Oct 3 21:17:32 2021 +0200

    Add new message in README.md

commit 88454a363c92b0198b41c86c6d6194c7ffe40d52 (origin/master, master)
Author: Name Surname <user@mail.com>
Date:   Thu Sep 30 05:50:57 2021 +0200

    Add link to Example 1
```

Now just, compare commit date and message (should not be the same).

To push changes use `--force` option: `git push -f` or push into new branch.
