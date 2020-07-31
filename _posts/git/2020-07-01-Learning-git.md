---
layout: post
title: "Learning Git"
comments: true
categories: git
---

## Learning Git


The “fatal: refusing to merge unrelated histories” Git error

Solution
```
git pull origin master --allow-unrelated-histories
```

Set Up stream
```
git checkout mybranch
git branch --set-upstream-to=origin/mybranch
```