[maximilian schwartzmueller github actions](https://www.udemy.com/course/github-actions-the-complete-guide/learn/lecture/34122306#learning-tools)

- HEAD points at latest commit 
- log older changes than what is checked out
```sh
git log
```
- checkout an earlier commit
```sh
git checkout <commit-hash> 
```
- go back to the branch with all the commits
```sh
git checkout main
# HEAD -> main
```
- revert a commit 
	- creates a new commit that undoes the actions of a specific commit (it's an 'undo' commit)
```sh
git revert <commit-hash>
```
- delete a commit 
	- it will remove all commits after a specific commit (returns you to a commit history before that commit and only the history preceding it)
```sh
git reset --hard <commit-hash>
```
- upload and downlaod  code 
```sh
git push & pull
```

