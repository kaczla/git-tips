# Example 2

Goal: add empty (without changes) commit (with message only)

# Steps

At beginning `git log` returns:

```text
commit 88454a363c92b0198b41c86c6d6194c7ffe40d52 (origin/master, master, HEAD -> commit_empty, origin/commit_empty)
Author: Name Surname <user@mail.com>
Date:   Thu Sep 30 05:50:57 2021 +0200

    Add link to Example 1
```

Next, add empty (without changes) commit (with message only) by command: `git commit -m "[pre-release] Test docker image" --allow-empty`

And, now `git log` returns:

```
commit ae716f8843d93776cdb3af8937d256ae635cc4f9 (HEAD -> commit_empty, origin/commit_empty)
Author: Name Surname <user@mail.com>
Date:   Sun Oct 3 21:28:29 2021 +0200

    [pre-release] Test docker image

commit 88454a363c92b0198b41c86c6d6194c7ffe40d52 (origin/master, master)
Author: Name Surname <user@mail.com>
Date:   Thu Sep 30 05:50:57 2021 +0200

    Add link to Example 1
```

To be sure that there were no changes, run command: `git diff HEAD~1` (should return empty).
