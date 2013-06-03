---
layout: post
title: "Who's the top commiter?"
date: 2013-04-15 17:16
comments: true
categories: git
---

Working on a large project with a team of developers and want to know how big your contribution is? Here is a simple way to do just that.

```
  git shortlog <branch name> --numbered --summary
```

Shortened version example.

```
  git shortlog master -n -s
```

This will show you the number of commits.

```
  1764  Chris Holmes
  1612  Joe Bloggs
```
