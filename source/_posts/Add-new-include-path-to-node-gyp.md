---
title: Add new include path to node-gyp
tags: []
number: 8
date: 2017-05-03 09:58:36
---

```
export INCLUDE_PATH=$INCLUDE_PATH:new/include/path

export CPATH="$INCLUDE_PATH"

export CPPPATH="$INCLUDE_PATH"
```