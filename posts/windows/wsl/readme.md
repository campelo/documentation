---
title: Reset wsl user's password
published: true
description: Reset wsl user's password
tags: 'wsl, root, password, linux'
cover_image: ../../assets/cover.png
canonical_url: null
id: 1584404
---

###### :postbox: Contact :brazil: :us: :fr:

[Twitter](https://twitter.com/campelo87)
[LinkedIn](https://www.linkedin.com/in/flavio-campelo/?locale=en_US)

---

# Reset wsl user's password

Open cmd.exe
```
# Display a list of distros.
wsl -l 

# Open a connects at distro with a specified user
wsl -u my-user -d my-distro

# Change user password
passwd my-user

# Quit distro
exit
```

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.