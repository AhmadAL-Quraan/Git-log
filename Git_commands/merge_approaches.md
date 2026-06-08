
# Merging approaches

### Merge 
```
git switch main
git fetch origin 
git merge origin/main
```
* When the branches have diverged, Git creates a new merge commit that has both branches as parents.
```
Before: 

A---B---C main
     \
      D---E feature

After: 
A---B---C--------M main
     \          /
      D---E---- feature
```

### Rebase 
```
git switch feature_branch
git rebase <target branch(top of it)>
git rebase main

```
* Advanced merge, instead of making a new commit, you take a whole commits of a branch (feature branch), and add them in-front of the main one, so the history of it will be linear. 
* This is very useful if u want to make several features for a main branch without the main history being affected.

```
Before: 

A---B---C main
     \
      D---E feature
After: 
A---B---C---D'---E' feature
```
### Squash 
`git rebase -i`

* An interactive window will appears after.

| Command  | Meaning                             |
| -------- | ----------------------------------- |
| `pick`   | keep commit normally                |
| `squash` | combine with previous commit        |
| `fixup`  | combine and discard message         |
| `reword` | keep commit but edit message        |
| `drop`   | remove commit                       |
| `edit`   | stop during rebase to modify commit |
* squash combines multiple commits into a single commit.
* It’s commonly used to clean up a feature branch before merging it into main.

==> After editing another window will appear for commit message.
```
Suppose your feature branch has many small commits:
A---B---C main
         \
          D---E---F feature
Where:

D = initial feature
E = fix typo
F = debugging changes

You may not want all these commits in the main history.

git checkout main
git merge --squash feature
git commit

Result: 
A---B---C---S main
```


| Operation | What happens                             |
| --------- | ---------------------------------------- |
| Merge     | Combines histories with a merge commit   |
| Rebase    | Replays commits on top of another branch |
| Squash    | Combines multiple commits into one       |



### Squash merging 

* Squash and merge into main directly.
```
git merge --squash feature
git commit
```

Result: 
```
A---B---C---S
```

It’s basically:

“Take all changes from this branch and make them one commit.”
