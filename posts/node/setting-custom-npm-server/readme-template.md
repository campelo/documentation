---
title: Node - Setting a custom npm server
published: true
description: Setting a custom npm server
tags: 'npm, custom, private, server'
cover_image: ../../assets/cover.png
canonical_url: null
id: 951870
date: '2022-01-11T18:53:04Z'
---

###### :postbox: Contact :brazil: :us: :fr:

[Twitter](https://twitter.com/campelo87)
[LinkedIn](https://www.linkedin.com/in/flavio-campelo/?locale=en_US)

---

## Setting a custom npm server

You can execute these commands [npm config](https://docs.npmjs.com/cli/v8/using-npm/config)

```PowerShell
npm config set registry https://mySite.com/private/repo-npm
 
npm config set strict-ssl false
```

or you can edit the file **```%userprofile%\.npmrc```** manually to change per-user config [npmrc docs](https://docs.npmjs.com/cli/v8/configuring-npm/npmrc)

```
registry=https://mySite.com/private/repo-npm
  
strict-ssl=false
```

## Typos or suggestions?

If you've found a typo, a sentence that could be improved or anything else that should be updated on this blog post, you can access it through a git repository and make a pull request. If you feel comfortable with github, instead of posting a comment, please go directly to https://github.com/campelo/documentation and open a new pull request with your changes.
