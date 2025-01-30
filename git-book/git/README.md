# git

## How to

### cherry-pick a range of commits

To include commits `A` through `B`

```sh
git cherry-pick A~..B
```

### Clean all ignored files

```sh
git clean -dfX
```

### Delete remove branch

```bash
git push -d <remote_name> <branchname>
```

### Find common ancestor

```bash
git merge-base <commit1> <commit2>
```

### Push a tag

```bash
git push origin tag <tag-name>
```

### See files in untracked directories

```bash
git status -u
```
