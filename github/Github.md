### Git Log and Commits
- git log to check commit history
- git checkout commit-hash to return to a commit 
- get checkout branch-name to return HEAD to the last commit in the branch

```sh
git log
git checkout f3ac63ffc8336079dc0a732c948bffdb846c753f
git log # does not show cany commits except for the ones before this
git checkout main
git log # shows call commits (we are back on main at the last commit)
```

### Git Branch

```sh
git branch feat-branch
git branch
git checkout feat-branch
```

- once a new branch is created (as a copy of main), we can checkout that new branch and HEAD will point to that second-branch, which is on the same commit as main
	- git HEAD points to the commit indirectly via branch 
		- in case of detached HEAD state (HEAD points to an earlier commit) no changes will be persisted
```shell
$ git log
commit 052b88404b5a3d7a8f8f56b272128d2609e22cfe (HEAD -> second-branch, main)
Author: bronifty <bronifty@gmail.com>
Date:   Mon Oct 23 15:56:23 2023 -0400

    added second-commit.md file

commit 974983ad8c8d6143a564aa2e548f45a2d15bedd8
Author: bronifty <bronifty@gmail.com>
Date:   Sun Oct 22 18:10:40 2023 -0400

    added README.md
```

- git checkout -b branch-name
```sh
bronifty@ubuntu:~/codes/deleteme$ git checkout -b third-branch
Switched to a new branch 'third-branch'
bronifty@ubuntu:~/codes/deleteme$ git branch
  main
  second-branch
* third-branch
```

- git checkout main and merge third branch changes
```sh
git checkout main
bronifty@ubuntu:~/codes/deleteme$ git merge third-branch
Updating 974983a..4759134
Fast-forward
 second-file.md | 0
 third-file.md  | 0
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 second-file.md
 create mode 100644 third-file.md
bronifty@ubuntu:~/codes/deleteme$ git log
commit 47591344b9b5e4bf2102e1f25da6f9bb97f60a06 (HEAD -> main, third-branch)
Author: bronifty <bronifty@gmail.com>
Date:   Mon Oct 23 16:45:12 2023 -0400

    added third-file.md

commit c01d749d88c4b774d30dbf739c408948c73d56f2 (second-branch)
Author: bronifty <bronifty@gmail.com>
Date:   Mon Oct 23 16:39:37 2023 -0400

    added second file.md

commit 974983ad8c8d6143a564aa2e548f45a2d15bedd8
Author: bronifty <bronifty@gmail.com>
Date:   Sun Oct 22 18:10:40 2023 -0400

    added README.md
```
- now main has cumulative changes of all branches since branch 3 had all cumulative changes
- if we checkout a specific commit, we will have a detached HEAD
```sh
bronifty@ubuntu:~/codes/deleteme$ git checkout c01d749d88c4b774d30dbf739c408948c73d56f2
Note: switching to 'c01d749d88c4b774d30dbf739c408948c73d56f2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at c01d749 added second file.md
bronifty@ubuntu:~/codes/deleteme$ git log
commit c01d749d88c4b774d30dbf739c408948c73d56f2 (HEAD, second-branch)
Author: bronifty <bronifty@gmail.com>
Date:   Mon Oct 23 16:39:37 2023 -0400

    added second file.md

commit 974983ad8c8d6143a564aa2e548f45a2d15bedd8
Author: bronifty <bronifty@gmail.com>
Date:   Sun Oct 22 18:10:40 2023 -0400

    added README.md
bronifty@ubuntu:~/codes/deleteme$ git checkout second-branch
Switched to branch 'second-branch'
bronifty@ubuntu:~/codes/deleteme$ git log
commit c01d749d88c4b774d30dbf739c408948c73d56f2 (HEAD -> second-branch)
Author: bronifty <bronifty@gmail.com>
Date:   Mon Oct 23 16:39:37 2023 -0400

    added second file.md

commit 974983ad8c8d6143a564aa2e548f45a2d15bedd8
Author: bronifty <bronifty@gmail.com>
Date:   Sun Oct 22 18:10:40 2023 -0400

    added README.md
```

