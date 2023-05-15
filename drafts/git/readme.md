---
title: 
published: false
description: 
tags: ''
cover_image: ../../assets/cover.png
canonical_url: null
id: 
---

###### :postbox: Contact :brazil: :us: :fr:

[Twitter](https://twitter.com/campelo87)
[LinkedIn](https://www.linkedin.com/in/flavio-campelo/?locale=en_US)

---

## Stash

```bash
git stash save "description"
git stash list
git stash apply 3 *3 represents the stash id*
git fetch --prune
git checkout -b newLocalBranchName
git checkout --track origin/newLocalBranchName
git merge origin/remoteBranchName
git push origin localBranchName:newRemoteBranchName
```

```bash
git archive --format=zip -o `<file-name>.zip` HEAD $(git diff-tree --no-commit-id --name-only --diff-filter=d -r HEAD)
```

**archive** compress files in a compressed folder
**--format=zip** compressed file format
**`<file-name>.zip`** compressed file name
**HEAD** 

**diff-tree** show commited files
**--no-commit-id** doesn't show commit id
**--name-only** shows only file names (not status)
**--diff-filter=d** filter commit status. **D** includes DELETED **d** excludes DELETED. Other status (A)dded (M)odified (D)eleted
**-r** recursive to show all files inside directories
**HEAD**

## Revert commit

For this scenario, we want to revert all commits after **B** commit

Current:
```
A <- B <- C <- D <- E <- HEAD
```

Expected:
```
A <- B <- HEAD
```

So we can do that doing this.

```bash
git reset --hard abc123 # abc123 is B commit identifier...
git reset --soft def456 # def456 is HEAD commit identifier...
git commit -m "Comming back to abc123"
```

## Sources

[git-archive](https://git-scm.com/docs/git-archive)

[git-diff-tree](https://git-scm.com/docs/git-diff-tree)

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.