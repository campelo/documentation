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

## Alias
```bash
alias # it will show all alias
alias name # it will show the alias for 'name' command
alias name='my command here' # it will set a new 'name' alias that it will execute the command 'my command here'
```

## Find
```bash
find /dir/to/search -name "file name" -print # it will show all files called "file name" for the folder '/dir/to/search'
find /dir/to/search -name "file name" -print 2>/dev/null # 2>/dev/null will redirect all errors to /dev/null
find /dir/to/search -name "file name" -print 2>&1 | grep -v "Permission denied" # 2>&1 will redirect all errors to the screen while grep will ignore all messages containing "Permission denied"
```

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.